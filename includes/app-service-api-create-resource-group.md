<span data-ttu-id="b4000-101">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b4000-101">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="b4000-102">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="b4000-102">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="b4000-103">Чтобы просмотреть доступные расположения, выполните команду `az appservice list-locations`.</span><span class="sxs-lookup"><span data-stu-id="b4000-103">To see the available locations, run the `az appservice list-locations` command.</span></span> <span data-ttu-id="b4000-104">Обычно ресурсы создаются в ближайших регионах.</span><span class="sxs-lookup"><span data-stu-id="b4000-104">You generally create resources in a region near you.</span></span>
