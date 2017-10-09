<span data-ttu-id="e9ec9-101">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e9ec9-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="e9ec9-102">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westeurope* расположение.</span><span class="sxs-lookup"><span data-stu-id="e9ec9-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="e9ec9-103">Обычно создают ресурс группы и hello ресурсы в области рядом с вами.</span><span class="sxs-lookup"><span data-stu-id="e9ec9-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="e9ec9-104">расположения toosee поддерживается для веб-приложений Azure, выполните hello `az appservice list-locations` команды.</span><span class="sxs-lookup"><span data-stu-id="e9ec9-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
