<span data-ttu-id="75698-101">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="75698-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="75698-102">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westeurope* расположение.</span><span class="sxs-lookup"><span data-stu-id="75698-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="75698-103">toosee hello доступных расположений, запустите hello `az appservice list-locations` команды.</span><span class="sxs-lookup"><span data-stu-id="75698-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="75698-104">Обычно ресурсы создаются в ближайших регионах.</span><span class="sxs-lookup"><span data-stu-id="75698-104">You generally create resources in a region near you.</span></span>
