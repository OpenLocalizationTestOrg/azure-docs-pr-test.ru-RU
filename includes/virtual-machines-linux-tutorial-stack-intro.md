## <a name="create-a-resource-group"></a><span data-ttu-id="1ac7a-101">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="1ac7a-101">Create a resource group</span></span>

<span data-ttu-id="1ac7a-102">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="1ac7a-103">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="1ac7a-104">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="1ac7a-105">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1ac7a-105">Create a virtual machine</span></span>

<span data-ttu-id="1ac7a-106">Создайте виртуальную Машину с hello [создания виртуальной машины az](/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="1ac7a-107">Hello следующий пример создает Виртуальную машину с именем *myVM* и создает ключи SSH, если они еще не существуют в ключевое расположение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="1ac7a-108">toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="1ac7a-109">При создании виртуальной Машины hello hello Azure CLI показано toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="1ac7a-110">Запишите hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="1ac7a-111">Этот адрес будет hello используется tooaccess виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-111">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="1ac7a-112">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="1ac7a-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="1ac7a-113">По умолчанию виртуальные машины Linux, развернутые в Azure, поддерживают только SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="1ac7a-114">Поскольку эта виртуальная машина будет toobe веб-сервер, вам потребуется tooopen порту 80 из hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="1ac7a-115">Используйте hello [az виртуальной машины откройте порт-](/cli/azure/vm#open-port) команда tooopen hello требуемого порта.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="1ac7a-116">SSH-подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="1ac7a-116">SSH into your VM</span></span>


<span data-ttu-id="1ac7a-117">Если вы еще не знаете Здравствуйте общедоступный IP-адрес виртуальной машины, запуска hello [список открытый ip-сетей az](/cli/azure/network/public-ip#list) команды:</span><span class="sxs-lookup"><span data-stu-id="1ac7a-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="1ac7a-118">Используйте hello следующая команда toocreate сеанс SSH с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="1ac7a-119">Замените hello открытый IP-адрес виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="1ac7a-120">В этом примере hello IP-адрес — *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="1ac7a-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

