---
title: "Функции развертывания для шаблонов Azure Resource Manager | Документация Майкрософт"
description: "Описывает функции, используемые в шаблоне Azure Resource Manager для получения сведений о развертывании."
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
ms.openlocfilehash: d7e6bcd669d40cb19de44b646505856ecd8f51a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="dc455-103">Функции развертывания для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc455-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="dc455-104">Диспетчер ресурсов предоставляет следующие функции для получения значений из разделов шаблонов и значений, связанных с развертыванием:</span><span class="sxs-lookup"><span data-stu-id="dc455-104">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="dc455-105">deployment</span><span class="sxs-lookup"><span data-stu-id="dc455-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="dc455-106">parameters</span><span class="sxs-lookup"><span data-stu-id="dc455-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="dc455-107">variables</span><span class="sxs-lookup"><span data-stu-id="dc455-107">variables</span></span>](#variables)

<span data-ttu-id="dc455-108">Сведения о получении значений из ресурсов, групп ресурсов или подписки см. в разделе [Функции для работы с ресурсами](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="dc455-108">To get values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="dc455-109">Развертывание</span><span class="sxs-lookup"><span data-stu-id="dc455-109">deployment</span></span>
`deployment()`

<span data-ttu-id="dc455-110">Возвращает сведения о текущей операции развертывания.</span><span class="sxs-lookup"><span data-stu-id="dc455-110">Returns information about the current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="dc455-111">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dc455-111">Return value</span></span>

<span data-ttu-id="dc455-112">Эта функция возвращает объект, который передается во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="dc455-112">This function returns the object that is passed during deployment.</span></span> <span data-ttu-id="dc455-113">Свойства в возвращаемом объекте зависят от того, передается ли объект развертывания в виде ссылки или встроенного объекта.</span><span class="sxs-lookup"><span data-stu-id="dc455-113">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="dc455-114">Когда объект развертывания передается встроенным (например, при использовании параметра **-TemplateFile** в Azure PowerShell для определения локального файла), формат возвращаемого объекта будет таким:</span><span class="sxs-lookup"><span data-stu-id="dc455-114">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span></span>

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

<span data-ttu-id="dc455-115">Когда объект передается в виде ссылки, как, например, при использовании параметра **-TemplateUri** для указания на удаленный объект, объект возвращается в следующем формате.</span><span class="sxs-lookup"><span data-stu-id="dc455-115">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span></span> 

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

### <a name="remarks"></a><span data-ttu-id="dc455-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="dc455-116">Remarks</span></span>

<span data-ttu-id="dc455-117">Вы можете использовать deployment() для ссылки на другой шаблон в зависимости от URI родительского шаблона.</span><span class="sxs-lookup"><span data-stu-id="dc455-117">You can use deployment() to link to another template based on the URI of the parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="dc455-118">Пример</span><span class="sxs-lookup"><span data-stu-id="dc455-118">Example</span></span>

<span data-ttu-id="dc455-119">В следующем примере возвращается объект развертывания:</span><span class="sxs-lookup"><span data-stu-id="dc455-119">The following example returns the deployment object:</span></span>

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

<span data-ttu-id="dc455-120">В предыдущем примере возвращается следующий объект:</span><span class="sxs-lookup"><span data-stu-id="dc455-120">The preceding example returns the following object:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="dc455-121">parameters</span><span class="sxs-lookup"><span data-stu-id="dc455-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="dc455-122">Возвращает значение параметра.</span><span class="sxs-lookup"><span data-stu-id="dc455-122">Returns a parameter value.</span></span> <span data-ttu-id="dc455-123">Указанное имя параметра должно быть определено в разделе параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="dc455-123">The specified parameter name must be defined in the parameters section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="dc455-124">Параметры</span><span class="sxs-lookup"><span data-stu-id="dc455-124">Parameters</span></span>

| <span data-ttu-id="dc455-125">Параметр</span><span class="sxs-lookup"><span data-stu-id="dc455-125">Parameter</span></span> | <span data-ttu-id="dc455-126">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dc455-126">Required</span></span> | <span data-ttu-id="dc455-127">Тип</span><span class="sxs-lookup"><span data-stu-id="dc455-127">Type</span></span> | <span data-ttu-id="dc455-128">Описание</span><span class="sxs-lookup"><span data-stu-id="dc455-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dc455-129">имя_параметра</span><span class="sxs-lookup"><span data-stu-id="dc455-129">parameterName</span></span> |<span data-ttu-id="dc455-130">Да</span><span class="sxs-lookup"><span data-stu-id="dc455-130">Yes</span></span> |<span data-ttu-id="dc455-131">string</span><span class="sxs-lookup"><span data-stu-id="dc455-131">string</span></span> |<span data-ttu-id="dc455-132">Имя параметра, который требуется вернуть.</span><span class="sxs-lookup"><span data-stu-id="dc455-132">The name of the parameter to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dc455-133">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dc455-133">Return value</span></span>

<span data-ttu-id="dc455-134">Значение указанного параметра.</span><span class="sxs-lookup"><span data-stu-id="dc455-134">The value of the specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="dc455-135">Примечания</span><span class="sxs-lookup"><span data-stu-id="dc455-135">Remarks</span></span>

<span data-ttu-id="dc455-136">Как правило, параметры используются, чтобы задать значения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="dc455-136">Typically, you use parameters to set resource values.</span></span> <span data-ttu-id="dc455-137">В следующем примере значению параметра задается имя веб-сайта, переданное во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="dc455-137">The following example sets the name of web site to the parameter value passed in during deployment.</span></span>

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

### <a name="example"></a><span data-ttu-id="dc455-138">Пример</span><span class="sxs-lookup"><span data-stu-id="dc455-138">Example</span></span>

<span data-ttu-id="dc455-139">В следующем примере показано упрощенное использование функции parameters.</span><span class="sxs-lookup"><span data-stu-id="dc455-139">The following example shows a simplified use of the parameters function.</span></span>

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

<span data-ttu-id="dc455-140">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="dc455-140">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="dc455-141">Имя</span><span class="sxs-lookup"><span data-stu-id="dc455-141">Name</span></span> | <span data-ttu-id="dc455-142">Тип</span><span class="sxs-lookup"><span data-stu-id="dc455-142">Type</span></span> | <span data-ttu-id="dc455-143">Значение</span><span class="sxs-lookup"><span data-stu-id="dc455-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dc455-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="dc455-144">stringOutput</span></span> | <span data-ttu-id="dc455-145">Строка</span><span class="sxs-lookup"><span data-stu-id="dc455-145">String</span></span> | <span data-ttu-id="dc455-146">вариант 1</span><span class="sxs-lookup"><span data-stu-id="dc455-146">option 1</span></span> |
| <span data-ttu-id="dc455-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="dc455-147">intOutput</span></span> | <span data-ttu-id="dc455-148">int</span><span class="sxs-lookup"><span data-stu-id="dc455-148">Int</span></span> | <span data-ttu-id="dc455-149">1</span><span class="sxs-lookup"><span data-stu-id="dc455-149">1</span></span> |
| <span data-ttu-id="dc455-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="dc455-150">objectOutput</span></span> | <span data-ttu-id="dc455-151">Объект</span><span class="sxs-lookup"><span data-stu-id="dc455-151">Object</span></span> | <span data-ttu-id="dc455-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="dc455-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="dc455-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="dc455-153">arrayOutput</span></span> | <span data-ttu-id="dc455-154">Массив,</span><span class="sxs-lookup"><span data-stu-id="dc455-154">Array</span></span> | <span data-ttu-id="dc455-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="dc455-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="dc455-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="dc455-156">crossOutput</span></span> | <span data-ttu-id="dc455-157">Строка</span><span class="sxs-lookup"><span data-stu-id="dc455-157">String</span></span> | <span data-ttu-id="dc455-158">вариант 1</span><span class="sxs-lookup"><span data-stu-id="dc455-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="dc455-159">variables</span><span class="sxs-lookup"><span data-stu-id="dc455-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="dc455-160">Возвращает значение переменной.</span><span class="sxs-lookup"><span data-stu-id="dc455-160">Returns the value of variable.</span></span> <span data-ttu-id="dc455-161">Указанное имя переменной должно быть определено в разделе переменных шаблона.</span><span class="sxs-lookup"><span data-stu-id="dc455-161">The specified variable name must be defined in the variables section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="dc455-162">Параметры</span><span class="sxs-lookup"><span data-stu-id="dc455-162">Parameters</span></span>

| <span data-ttu-id="dc455-163">Параметр</span><span class="sxs-lookup"><span data-stu-id="dc455-163">Parameter</span></span> | <span data-ttu-id="dc455-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dc455-164">Required</span></span> | <span data-ttu-id="dc455-165">Тип</span><span class="sxs-lookup"><span data-stu-id="dc455-165">Type</span></span> | <span data-ttu-id="dc455-166">Описание</span><span class="sxs-lookup"><span data-stu-id="dc455-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dc455-167">variableName</span><span class="sxs-lookup"><span data-stu-id="dc455-167">variableName</span></span> |<span data-ttu-id="dc455-168">Да</span><span class="sxs-lookup"><span data-stu-id="dc455-168">Yes</span></span> |<span data-ttu-id="dc455-169">Строка</span><span class="sxs-lookup"><span data-stu-id="dc455-169">String</span></span> |<span data-ttu-id="dc455-170">Имя переменной, которую необходимо вернуть.</span><span class="sxs-lookup"><span data-stu-id="dc455-170">The name of the variable to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dc455-171">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dc455-171">Return value</span></span>

<span data-ttu-id="dc455-172">Значение указанной переменной.</span><span class="sxs-lookup"><span data-stu-id="dc455-172">The value of the specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="dc455-173">Примечания</span><span class="sxs-lookup"><span data-stu-id="dc455-173">Remarks</span></span>

<span data-ttu-id="dc455-174">Как правило, переменные используются, чтобы упростить шаблон за счет создания сложных значений (единожды).</span><span class="sxs-lookup"><span data-stu-id="dc455-174">Typically, you use variables to simplify your template by constructing complex values only once.</span></span> <span data-ttu-id="dc455-175">В примере ниже создается уникальное имя для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="dc455-175">The following example constructs a unique name for a storage account.</span></span>

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

### <a name="example"></a><span data-ttu-id="dc455-176">Пример</span><span class="sxs-lookup"><span data-stu-id="dc455-176">Example</span></span>

<span data-ttu-id="dc455-177">Пример шаблона возвращает разные значения переменных.</span><span class="sxs-lookup"><span data-stu-id="dc455-177">The example template returns different variable values.</span></span>

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

<span data-ttu-id="dc455-178">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="dc455-178">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="dc455-179">Имя</span><span class="sxs-lookup"><span data-stu-id="dc455-179">Name</span></span> | <span data-ttu-id="dc455-180">Тип</span><span class="sxs-lookup"><span data-stu-id="dc455-180">Type</span></span> | <span data-ttu-id="dc455-181">Значение</span><span class="sxs-lookup"><span data-stu-id="dc455-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dc455-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="dc455-182">exampleOutput1</span></span> | <span data-ttu-id="dc455-183">Строка</span><span class="sxs-lookup"><span data-stu-id="dc455-183">String</span></span> | <span data-ttu-id="dc455-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="dc455-184">myVariable</span></span> |
| <span data-ttu-id="dc455-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="dc455-185">exampleOutput2</span></span> | <span data-ttu-id="dc455-186">Массив,</span><span class="sxs-lookup"><span data-stu-id="dc455-186">Array</span></span> | <span data-ttu-id="dc455-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="dc455-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="dc455-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="dc455-188">exampleOutput3</span></span> | <span data-ttu-id="dc455-189">Строка</span><span class="sxs-lookup"><span data-stu-id="dc455-189">String</span></span> | <span data-ttu-id="dc455-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="dc455-190">myVariable</span></span> |
| <span data-ttu-id="dc455-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="dc455-191">exampleOutput4</span></span> |  <span data-ttu-id="dc455-192">Объект</span><span class="sxs-lookup"><span data-stu-id="dc455-192">Object</span></span> | <span data-ttu-id="dc455-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="dc455-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dc455-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc455-194">Next steps</span></span>
* <span data-ttu-id="dc455-195">Описание разделов в шаблоне Azure Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dc455-195">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="dc455-196">Инструкции по объединению нескольких шаблонов см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dc455-196">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="dc455-197">Указания по выполнению заданного количества циклов итерации при создании типа ресурса см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="dc455-197">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="dc455-198">Указания по развертыванию созданного шаблона см. в статье, посвященной [развертыванию приложения с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="dc455-198">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

