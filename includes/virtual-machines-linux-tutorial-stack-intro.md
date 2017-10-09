## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Создание виртуальной машины

Создайте виртуальную Машину с hello [создания виртуальной машины az](/cli/azure/vm#create) команды. 

Hello следующий пример создает Виртуальную машину с именем *myVM* и создает ключи SSH, если они еще не существуют в ключевое расположение по умолчанию. toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

При создании виртуальной Машины hello hello Azure CLI показано toohello аналогичные сведения, следующий пример. Запишите hello `publicIpAddress`. Этот адрес будет hello используется tooaccess виртуальной Машины.

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

По умолчанию виртуальные машины Linux, развернутые в Azure, поддерживают только SSH-подключения. Поскольку эта виртуальная машина будет toobe веб-сервер, вам потребуется tooopen порту 80 из hello Интернета. Используйте hello [az виртуальной машины откройте порт-](/cli/azure/vm#open-port) команда tooopen hello требуемого порта.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>SSH-подключение к виртуальной машине


Если вы еще не знаете Здравствуйте общедоступный IP-адрес виртуальной машины, запуска hello [список открытый ip-сетей az](/cli/azure/network/public-ip#list) команды:


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

Используйте hello следующая команда toocreate сеанс SSH с виртуальной машиной hello. Замените hello открытый IP-адрес виртуальной машины. В этом примере hello IP-адрес — *40.68.254.142*.

```bash
ssh azureuser@40.68.254.142
```

