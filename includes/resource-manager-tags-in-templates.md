<span data-ttu-id="a1162-101">tootag ресурсов во время развертывания, добавьте hello `tags` развертывании ресурсов toohello элемента.</span><span class="sxs-lookup"><span data-stu-id="a1162-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="a1162-102">Укажите имя тега hello и значение.</span><span class="sxs-lookup"><span data-stu-id="a1162-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="a1162-103">Применение имени тега toohello литеральное значение</span><span class="sxs-lookup"><span data-stu-id="a1162-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="a1162-104">Hello пример учетной записи хранилища с двумя тегами (`Dept` и `Environment`), которые задаются значения tooliteral:</span><span class="sxs-lookup"><span data-stu-id="a1162-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

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

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="a1162-105">Применение элемента объекта toohello тег</span><span class="sxs-lookup"><span data-stu-id="a1162-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="a1162-106">Можно определить параметр объекта, который хранит несколько тегов и применить объект toohello тега элемента.</span><span class="sxs-lookup"><span data-stu-id="a1162-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="a1162-107">Каждое свойство в объекте hello становится отдельный тег для ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="a1162-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="a1162-108">Hello следующий пример содержит параметр с именем `tagValues` , примененные toohello тег для элемента.</span><span class="sxs-lookup"><span data-stu-id="a1162-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

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

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="a1162-109">Применение имени тега toohello строка JSON</span><span class="sxs-lookup"><span data-stu-id="a1162-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="a1162-110">toostore много значений в один тэг, применить строку JSON, которое представляет значения hello.</span><span class="sxs-lookup"><span data-stu-id="a1162-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="a1162-111">вся строка JSON Hello сохраняется как один тег, который не может превышать 256 символов.</span><span class="sxs-lookup"><span data-stu-id="a1162-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="a1162-112">Hello следующий пример содержит один тег с именем `CostCenter` , содержащий несколько значений из строки JSON:</span><span class="sxs-lookup"><span data-stu-id="a1162-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

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