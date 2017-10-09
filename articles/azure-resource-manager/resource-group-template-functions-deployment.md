---
title: "функции шаблонов диспетчера ресурсов aaaAzure - развертывание | Документы Microsoft"
description: "Описывает toouse функции hello в сведения о развертывании шаблона tooretrieve диспетчера ресурсов Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="04ba3-103">Функции развертывания для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="04ba3-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="04ba3-104">Диспетчер ресурсов предоставляет hello следующие функции для получения значения из разделов шаблона hello и значения связанных toohello развертывания:</span><span class="sxs-lookup"><span data-stu-id="04ba3-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="04ba3-105">deployment</span><span class="sxs-lookup"><span data-stu-id="04ba3-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="04ba3-106">parameters</span><span class="sxs-lookup"><span data-stu-id="04ba3-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="04ba3-107">variables</span><span class="sxs-lookup"><span data-stu-id="04ba3-107">variables</span></span>](#variables)

<span data-ttu-id="04ba3-108">tooget значения из ресурсов, групп ресурсов или подписки, в разделе [функций ресурсов](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="04ba3-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="04ba3-109">Развертывание</span><span class="sxs-lookup"><span data-stu-id="04ba3-109">deployment</span></span>
`deployment()`

<span data-ttu-id="04ba3-110">Возвращает сведения о текущей операции развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="04ba3-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="04ba3-111">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="04ba3-111">Return value</span></span>

<span data-ttu-id="04ba3-112">Эта функция возвращает hello объекта, передаваемого во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="04ba3-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="04ba3-113">свойства Hello в hello, возвращенный объект зависят от ли hello объекта развертывания передается как ссылка или как объект в строку.</span><span class="sxs-lookup"><span data-stu-id="04ba3-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="04ba3-114">Hello объекта развертывания — при передаче в строки, например, при использовании hello **- TemplateFile** параметр в Azure PowerShell toopoint tooa локального файла, hello возвращается объект имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="04ba3-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="04ba3-115">Когда hello объекта передается в качестве ссылки, например, когда с помощью hello **- TemplateUri** параметр toopoint tooa удаленного объекта hello объекта возвращается в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="04ba3-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="04ba3-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="04ba3-116">Remarks</span></span>

<span data-ttu-id="04ba3-117">Можно использовать deployment() toolink tooanother шаблона, основанного на hello URI hello родительского шаблона.</span><span class="sxs-lookup"><span data-stu-id="04ba3-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="04ba3-118">Пример</span><span class="sxs-lookup"><span data-stu-id="04ba3-118">Example</span></span>

<span data-ttu-id="04ba3-119">Hello следующий пример возвращает hello объекта развертывания.</span><span class="sxs-lookup"><span data-stu-id="04ba3-119">hello following example returns hello deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="04ba3-120">Hello выше пример возвращает hello следующих объектов:</span><span class="sxs-lookup"><span data-stu-id="04ba3-120">hello preceding example returns hello following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="04ba3-121">parameters</span><span class="sxs-lookup"><span data-stu-id="04ba3-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="04ba3-122">Возвращает значение параметра.</span><span class="sxs-lookup"><span data-stu-id="04ba3-122">Returns a parameter value.</span></span> <span data-ttu-id="04ba3-123">Hello указанное имя параметра должен быть определен в разделе параметров hello hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="04ba3-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="04ba3-124">Параметры</span><span class="sxs-lookup"><span data-stu-id="04ba3-124">Parameters</span></span>

| <span data-ttu-id="04ba3-125">Параметр</span><span class="sxs-lookup"><span data-stu-id="04ba3-125">Parameter</span></span> | <span data-ttu-id="04ba3-126">Обязательно</span><span class="sxs-lookup"><span data-stu-id="04ba3-126">Required</span></span> | <span data-ttu-id="04ba3-127">Тип</span><span class="sxs-lookup"><span data-stu-id="04ba3-127">Type</span></span> | <span data-ttu-id="04ba3-128">Описание</span><span class="sxs-lookup"><span data-stu-id="04ba3-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="04ba3-129">имя_параметра</span><span class="sxs-lookup"><span data-stu-id="04ba3-129">parameterName</span></span> |<span data-ttu-id="04ba3-130">Да</span><span class="sxs-lookup"><span data-stu-id="04ba3-130">Yes</span></span> |<span data-ttu-id="04ba3-131">string</span><span class="sxs-lookup"><span data-stu-id="04ba3-131">string</span></span> |<span data-ttu-id="04ba3-132">Имя параметра tooreturn hello Hello.</span><span class="sxs-lookup"><span data-stu-id="04ba3-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="04ba3-133">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="04ba3-133">Return value</span></span>

<span data-ttu-id="04ba3-134">параметра указано значение Hello hello.</span><span class="sxs-lookup"><span data-stu-id="04ba3-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="04ba3-135">Примечания</span><span class="sxs-lookup"><span data-stu-id="04ba3-135">Remarks</span></span>

<span data-ttu-id="04ba3-136">Обычно используются значения ресурсов tooset параметров.</span><span class="sxs-lookup"><span data-stu-id="04ba3-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="04ba3-137">Hello следующем примере задается имя hello значение параметра toohello веб-узла, переданного во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="04ba3-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="04ba3-138">Пример</span><span class="sxs-lookup"><span data-stu-id="04ba3-138">Example</span></span>

<span data-ttu-id="04ba3-139">Hello пример упрощенного используйте параметры функции hello.</span><span class="sxs-lookup"><span data-stu-id="04ba3-139">hello following example shows a simplified use of hello parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="04ba3-140">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="04ba3-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="04ba3-141">Имя</span><span class="sxs-lookup"><span data-stu-id="04ba3-141">Name</span></span> | <span data-ttu-id="04ba3-142">Тип</span><span class="sxs-lookup"><span data-stu-id="04ba3-142">Type</span></span> | <span data-ttu-id="04ba3-143">Значение</span><span class="sxs-lookup"><span data-stu-id="04ba3-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="04ba3-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="04ba3-144">stringOutput</span></span> | <span data-ttu-id="04ba3-145">Строка</span><span class="sxs-lookup"><span data-stu-id="04ba3-145">String</span></span> | <span data-ttu-id="04ba3-146">вариант 1</span><span class="sxs-lookup"><span data-stu-id="04ba3-146">option 1</span></span> |
| <span data-ttu-id="04ba3-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="04ba3-147">intOutput</span></span> | <span data-ttu-id="04ba3-148">int</span><span class="sxs-lookup"><span data-stu-id="04ba3-148">Int</span></span> | <span data-ttu-id="04ba3-149">1</span><span class="sxs-lookup"><span data-stu-id="04ba3-149">1</span></span> |
| <span data-ttu-id="04ba3-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="04ba3-150">objectOutput</span></span> | <span data-ttu-id="04ba3-151">Объект</span><span class="sxs-lookup"><span data-stu-id="04ba3-151">Object</span></span> | <span data-ttu-id="04ba3-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="04ba3-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="04ba3-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="04ba3-153">arrayOutput</span></span> | <span data-ttu-id="04ba3-154">Массив,</span><span class="sxs-lookup"><span data-stu-id="04ba3-154">Array</span></span> | <span data-ttu-id="04ba3-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="04ba3-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="04ba3-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="04ba3-156">crossOutput</span></span> | <span data-ttu-id="04ba3-157">Строка</span><span class="sxs-lookup"><span data-stu-id="04ba3-157">String</span></span> | <span data-ttu-id="04ba3-158">вариант 1</span><span class="sxs-lookup"><span data-stu-id="04ba3-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="04ba3-159">variables</span><span class="sxs-lookup"><span data-stu-id="04ba3-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="04ba3-160">Возвращает hello значение переменной.</span><span class="sxs-lookup"><span data-stu-id="04ba3-160">Returns hello value of variable.</span></span> <span data-ttu-id="04ba3-161">Указанное имя переменной Hello должен быть определен в разделе переменные hello hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="04ba3-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="04ba3-162">Параметры</span><span class="sxs-lookup"><span data-stu-id="04ba3-162">Parameters</span></span>

| <span data-ttu-id="04ba3-163">Параметр</span><span class="sxs-lookup"><span data-stu-id="04ba3-163">Parameter</span></span> | <span data-ttu-id="04ba3-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="04ba3-164">Required</span></span> | <span data-ttu-id="04ba3-165">Тип</span><span class="sxs-lookup"><span data-stu-id="04ba3-165">Type</span></span> | <span data-ttu-id="04ba3-166">Описание</span><span class="sxs-lookup"><span data-stu-id="04ba3-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="04ba3-167">variableName</span><span class="sxs-lookup"><span data-stu-id="04ba3-167">variableName</span></span> |<span data-ttu-id="04ba3-168">Да</span><span class="sxs-lookup"><span data-stu-id="04ba3-168">Yes</span></span> |<span data-ttu-id="04ba3-169">Строка</span><span class="sxs-lookup"><span data-stu-id="04ba3-169">String</span></span> |<span data-ttu-id="04ba3-170">Имя переменной tooreturn hello Hello.</span><span class="sxs-lookup"><span data-stu-id="04ba3-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="04ba3-171">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="04ba3-171">Return value</span></span>

<span data-ttu-id="04ba3-172">значение указанной переменной hello Hello.</span><span class="sxs-lookup"><span data-stu-id="04ba3-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="04ba3-173">Примечания</span><span class="sxs-lookup"><span data-stu-id="04ba3-173">Remarks</span></span>

<span data-ttu-id="04ba3-174">Обычно используется toosimplify переменных шаблона, создав сложных значений только один раз.</span><span class="sxs-lookup"><span data-stu-id="04ba3-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="04ba3-175">Hello следующий пример создает уникальное имя для учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="04ba3-175">hello following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="04ba3-176">Пример</span><span class="sxs-lookup"><span data-stu-id="04ba3-176">Example</span></span>

<span data-ttu-id="04ba3-177">Пример шаблона Hello возвращает разные значения переменной.</span><span class="sxs-lookup"><span data-stu-id="04ba3-177">hello example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="04ba3-178">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="04ba3-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="04ba3-179">Имя</span><span class="sxs-lookup"><span data-stu-id="04ba3-179">Name</span></span> | <span data-ttu-id="04ba3-180">Тип</span><span class="sxs-lookup"><span data-stu-id="04ba3-180">Type</span></span> | <span data-ttu-id="04ba3-181">Значение</span><span class="sxs-lookup"><span data-stu-id="04ba3-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="04ba3-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="04ba3-182">exampleOutput1</span></span> | <span data-ttu-id="04ba3-183">Строка</span><span class="sxs-lookup"><span data-stu-id="04ba3-183">String</span></span> | <span data-ttu-id="04ba3-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="04ba3-184">myVariable</span></span> |
| <span data-ttu-id="04ba3-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="04ba3-185">exampleOutput2</span></span> | <span data-ttu-id="04ba3-186">Массив,</span><span class="sxs-lookup"><span data-stu-id="04ba3-186">Array</span></span> | <span data-ttu-id="04ba3-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="04ba3-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="04ba3-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="04ba3-188">exampleOutput3</span></span> | <span data-ttu-id="04ba3-189">Строка</span><span class="sxs-lookup"><span data-stu-id="04ba3-189">String</span></span> | <span data-ttu-id="04ba3-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="04ba3-190">myVariable</span></span> |
| <span data-ttu-id="04ba3-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="04ba3-191">exampleOutput4</span></span> |  <span data-ttu-id="04ba3-192">Объект</span><span class="sxs-lookup"><span data-stu-id="04ba3-192">Object</span></span> | <span data-ttu-id="04ba3-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="04ba3-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="04ba3-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="04ba3-194">Next steps</span></span>
* <span data-ttu-id="04ba3-195">Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="04ba3-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="04ba3-196">toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="04ba3-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="04ba3-197">tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="04ba3-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="04ba3-198">toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="04ba3-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

