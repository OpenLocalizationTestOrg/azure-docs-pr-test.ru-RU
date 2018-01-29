## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#az_group_create). Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Создание виртуальной машины

Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#az_vm_create). 

В следующем примере создаются виртуальная машина *myVM* и ключи SSH, если они не существуют в расположении ключей по умолчанию. Чтобы использовать определенный набор ключей, используйте параметр `--ssh-key-value`. Эта команда также задает *azureuser* в качестве имени пользователя администратора. Это имя будет использоваться для подключения к виртуальной машине. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

После создания виртуальной машины в Azure CLI отображается информация следующего вида. Запишите значение `publicIpAddress`. Этот адрес будет использоваться для доступа к виртуальной машине на следующих шагах.

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



## <a name="open-port-80-for-web-traffic"></a>Открытие порта 80 для веб-трафика 

По умолчанию виртуальные машины Linux, развернутые в Azure, поддерживают только SSH-подключения. Так как эта виртуальная машина будет использоваться в качестве веб-сервера, необходимо открыть порт 80 через Интернет. Выполните команду [az vm open-port](/cli/azure/vm#az_vm_open_port), чтобы открыть нужный порт.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>SSH-подключение к виртуальной машине


Если вам не известен общедоступный IP-адрес виртуальной машины, используйте команду [az network public-ip list](/cli/azure/network/public-ip#list). Этот IP-адрес необходим для выполнения нескольких следующих шагов.


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

Используйте следующую команду для создания сеанса SSH с виртуальной машиной. Укажите правильный общедоступный IP-адрес виртуальной машины. В этом примере это IP-адрес *40.68.254.142*. *azureuser* — это имя пользователя администратора, заданное при создании виртуальной машины.

```bash
ssh azureuser@40.68.254.142
```

