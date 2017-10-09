Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.

[!INCLUDE [resource group intro text](resource-group.md)]

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westeurope* расположение.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Обычно создают ресурс группы и hello ресурсы в области рядом с вами. расположения toosee поддерживается для веб-приложений Azure, выполните hello `az appservice list-locations` команды. 
