<span data-ttu-id="fa1c8-101">Для добавления тега к ресурсу во время развертывания добавьте элемент `tags` к развертываемому ресурсу</span><span class="sxs-lookup"><span data-stu-id="fa1c8-101">To tag a resource during deployment, add the `tags` element to the resource you are deploying.</span></span> <span data-ttu-id="fa1c8-102">и укажите имя и значение тега.</span><span class="sxs-lookup"><span data-stu-id="fa1c8-102">Provide the tag name and value.</span></span>

### <a name="apply-a-literal-value-to-the-tag-name"></a><span data-ttu-id="fa1c8-103">Применение литерального значения к имени тега</span><span class="sxs-lookup"><span data-stu-id="fa1c8-103">Apply a literal value to the tag name</span></span>
<span data-ttu-id="fa1c8-104">В следующем примере показана учетная запись хранения с двумя тегами (`Dept` и `Environment`), которым присвоены литеральные значения.</span><span class="sxs-lookup"><span data-stu-id="fa1c8-104">The following example shows a storage account with two tags (`Dept` and `Environment`) that are set to literal values:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-to-the-tag-element"></a><span data-ttu-id="fa1c8-105">Применение объекта к элементу тега</span><span class="sxs-lookup"><span data-stu-id="fa1c8-105">Apply an object to the tag element</span></span>
<span data-ttu-id="fa1c8-106">Можно определить параметр объекта, который хранит несколько тегов, и применить этот объект к элементу тега.</span><span class="sxs-lookup"><span data-stu-id="fa1c8-106">You can define an object parameter that stores several tags, and apply that object to the tag element.</span></span> <span data-ttu-id="fa1c8-107">Каждое свойство в объекте становится отдельным тегом ресурса.</span><span class="sxs-lookup"><span data-stu-id="fa1c8-107">Each property in the object becomes a separate tag for the resource.</span></span> <span data-ttu-id="fa1c8-108">В следующем примере содержится параметр с именем `tagValues`, который применяется к элементу тега.</span><span class="sxs-lookup"><span data-stu-id="fa1c8-108">The following example has a parameter named `tagValues` that is applied to the tag element.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-to-the-tag-name"></a><span data-ttu-id="fa1c8-109">Применение строки JSON к имени тега</span><span class="sxs-lookup"><span data-stu-id="fa1c8-109">Apply a JSON string to the tag name</span></span>

<span data-ttu-id="fa1c8-110">Для хранения большого количества значений в одном теге примените строку JSON, представляющую значения.</span><span class="sxs-lookup"><span data-stu-id="fa1c8-110">To store many values in a single tag, apply a JSON string that represents the values.</span></span> <span data-ttu-id="fa1c8-111">Вся строка JSON сохраняется как один тег, значение которого не может превышать 256 символов.</span><span class="sxs-lookup"><span data-stu-id="fa1c8-111">The entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="fa1c8-112">В следующем примере приведен один тег с именем `CostCenter`, содержащий несколько значений из строки JSON.</span><span class="sxs-lookup"><span data-stu-id="fa1c8-112">The following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```