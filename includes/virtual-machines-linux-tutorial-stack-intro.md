## <a name="create-a-resource-group"></a><span data-ttu-id="8955b-101">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="8955b-101">Create a resource group</span></span>

<span data-ttu-id="8955b-102">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8955b-102">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="8955b-103">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="8955b-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="8955b-104">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="8955b-104">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="8955b-105">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8955b-105">Create a virtual machine</span></span>

<span data-ttu-id="8955b-106">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="8955b-106">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="8955b-107">В следующем примере создаются виртуальная машина *myVM* и ключи SSH, если они не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8955b-107">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="8955b-108">Чтобы использовать определенный набор ключей, используйте параметр `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="8955b-108">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="8955b-109">После создания виртуальной машины в Azure CLI отображается информация следующего вида.</span><span class="sxs-lookup"><span data-stu-id="8955b-109">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="8955b-110">Запишите значение `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="8955b-110">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="8955b-111">Этот адрес используется для доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="8955b-111">This address is used to access the VM.</span></span>

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



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="8955b-112">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="8955b-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="8955b-113">По умолчанию виртуальные машины Linux, развернутые в Azure, поддерживают только SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="8955b-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="8955b-114">Так как эта виртуальная машина будет использоваться в качестве веб-сервера, необходимо открыть порт 80 через Интернет.</span><span class="sxs-lookup"><span data-stu-id="8955b-114">Because this VM is going to be a web server, you need to open port 80 from the internet.</span></span> <span data-ttu-id="8955b-115">Выполните команду [az vm open-port](/cli/azure/vm#open-port), чтобы открыть нужный порт.</span><span class="sxs-lookup"><span data-stu-id="8955b-115">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="8955b-116">SSH-подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="8955b-116">SSH into your VM</span></span>


<span data-ttu-id="8955b-117">Если вы не знаете общедоступный IP-адрес виртуальной машины, используйте команду [az network public-ip list](/cli/azure/network/public-ip#list):</span><span class="sxs-lookup"><span data-stu-id="8955b-117">If you don't already know the public IP address of your VM, run the [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="8955b-118">Используйте следующую команду для создания сеанса SSH с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="8955b-118">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="8955b-119">Укажите правильный общедоступный IP-адрес виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8955b-119">Substitute the correct public IP address of your virtual machine.</span></span> <span data-ttu-id="8955b-120">В этом примере это IP-адрес *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="8955b-120">In this example, the IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

