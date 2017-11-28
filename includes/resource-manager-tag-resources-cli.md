<span data-ttu-id="4752e-101">Чтобы добавить тег к группе ресурсов, используйте **набор групп Azure**.</span><span class="sxs-lookup"><span data-stu-id="4752e-101">To add a tag to a resource group, use **azure group set**.</span></span> <span data-ttu-id="4752e-102">Если у группы ресурсов нет тегов, передайте один.</span><span class="sxs-lookup"><span data-stu-id="4752e-102">If the resource group does not have any existing tags, pass in the tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="4752e-103">При этом обновляются все теги.</span><span class="sxs-lookup"><span data-stu-id="4752e-103">Tags are updated as a whole.</span></span> <span data-ttu-id="4752e-104">Если вы хотите добавить тег к группе ресурсов, в которой уже есть теги, передайте их все.</span><span class="sxs-lookup"><span data-stu-id="4752e-104">If you want to add a tag to a resource group that has existing tags, pass all the tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="4752e-105">Ресурсы не унаследуют теги в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4752e-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="4752e-106">Чтобы добавить тег к ресурсу, используйте **набор ресурсов Azure**.</span><span class="sxs-lookup"><span data-stu-id="4752e-106">To add a tag to a resource, use **azure resource set**.</span></span> <span data-ttu-id="4752e-107">Передайте номер версии API для типа ресурса, к которому добавляется тег.</span><span class="sxs-lookup"><span data-stu-id="4752e-107">Pass the API version number for the resource type that you are adding the tag to.</span></span> <span data-ttu-id="4752e-108">Если нужно получить версию API, используйте следующую команду, указав поставщик для настраиваемого типа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="4752e-108">If you need to retrieve the API version, use the following command with the resource provider for the type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="4752e-109">В результатах найдите нужный тип ресурса.</span><span class="sxs-lookup"><span data-stu-id="4752e-109">In the results, look for the resource type you want.</span></span>

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

<span data-ttu-id="4752e-110">Теперь укажите эту версию API, имя группы ресурсов, имя ресурса, тип ресурса и значение тега в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="4752e-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="4752e-111">Существующие теги находятся непосредственно в ресурсах и группах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4752e-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="4752e-112">Чтобы просмотреть существующие теги, запросите сведения о группе ресурсов и ее ресурсах с помощью команды **azure group show**.</span><span class="sxs-lookup"><span data-stu-id="4752e-112">To see the existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="4752e-113">Отобразятся метаданные о группе ресурсов, включая все примененные к ней теги.</span><span class="sxs-lookup"><span data-stu-id="4752e-113">Which returns metadata about the resource group, including any tags applied to it.</span></span>

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

<span data-ttu-id="4752e-114">Теги для конкретного ресурса можно просмотреть с помощью команды **azure resource show**.</span><span class="sxs-lookup"><span data-stu-id="4752e-114">You view the tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="4752e-115">Чтобы получить все ресурсы со значением тега, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4752e-115">To retrieve all the resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="4752e-116">Чтобы получить все группы ресурсов со значением тега, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4752e-116">To retrieve all the resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="4752e-117">Чтобы просмотреть существующие теги в подписке, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4752e-117">You can view the existing tags in your subscription with the following command:</span></span>

```azurecli
azure tag list
```
