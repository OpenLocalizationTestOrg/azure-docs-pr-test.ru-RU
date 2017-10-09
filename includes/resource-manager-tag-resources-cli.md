<span data-ttu-id="e0bff-101">использовать tooadd группу ресурсов тег tooa **набор групп azure**.</span><span class="sxs-lookup"><span data-stu-id="e0bff-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="e0bff-102">Если группа ресурсов hello не имеет существующие теги, передайте тег hello.</span><span class="sxs-lookup"><span data-stu-id="e0bff-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="e0bff-103">При этом обновляются все теги.</span><span class="sxs-lookup"><span data-stu-id="e0bff-103">Tags are updated as a whole.</span></span> <span data-ttu-id="e0bff-104">Если вы хотите tooadd группу ресурсов tooa тег с существующие теги, передайте все теги hello.</span><span class="sxs-lookup"><span data-stu-id="e0bff-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="e0bff-105">Ресурсы не унаследуют теги в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e0bff-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="e0bff-106">использовать tooadd ресурс tooa тег **набор ресурсов azure**.</span><span class="sxs-lookup"><span data-stu-id="e0bff-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="e0bff-107">Передайте hello номер версии API для hello тип ресурса, который вы добавляете тег hello.</span><span class="sxs-lookup"><span data-stu-id="e0bff-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="e0bff-108">При необходимости tooretrieve hello API версии используйте следующую команду с поставщиком ресурсов hello для типа hello установки hello:</span><span class="sxs-lookup"><span data-stu-id="e0bff-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="e0bff-109">В результатах hello поиск нужного типа ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="e0bff-109">In hello results, look for hello resource type you want.</span></span>

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

<span data-ttu-id="e0bff-110">Теперь укажите эту версию API, имя группы ресурсов, имя ресурса, тип ресурса и значение тега в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="e0bff-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="e0bff-111">Существующие теги находятся непосредственно в ресурсах и группах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e0bff-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="e0bff-112">существующие теги hello toosee получить группу ресурсов и его ресурсы с **Показать группу azure**.</span><span class="sxs-lookup"><span data-stu-id="e0bff-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="e0bff-113">Которая возвращает метаданные о hello группы ресурсов, включая любые теги, примененные tooit.</span><span class="sxs-lookup"><span data-stu-id="e0bff-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

<span data-ttu-id="e0bff-114">Просмотр hello тегов для определенного ресурса с помощью **Показать ресурсов azure**.</span><span class="sxs-lookup"><span data-stu-id="e0bff-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="e0bff-115">tooretrieve использовать все ресурсы hello со значением тега:</span><span class="sxs-lookup"><span data-stu-id="e0bff-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="e0bff-116">Используйте для всех групп ресурсов hello со значением тега tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="e0bff-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="e0bff-117">Можно просматривать существующие теги hello в вашей подписке на hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e0bff-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
