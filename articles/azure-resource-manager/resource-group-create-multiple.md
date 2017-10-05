---
title: "Развертывание нескольких экземпляров ресурсов Azure | Документация Майкрософт"
description: "Использование операции копирования и массивов в шаблоне диспетчера ресурсов Azure для выполнения нескольких итераций при развертывании ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: ed8e3081d2b2e07938d7cf3aa5f95f6dde81bc66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="e0921-103">Развертывание нескольких экземпляров ресурса или свойства в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e0921-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="e0921-104">В этом разделе показано, как выполнить итерацию в шаблоне Azure Resource Manager для создания нескольких экземпляров ресурса или нескольких экземпляров свойства ресурса.</span><span class="sxs-lookup"><span data-stu-id="e0921-104">This topic shows you how to iterate in your Azure Resource Manager template to create multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="e0921-105">Если необходимо добавить логику в шаблон, чтобы указать, развертывается ли ресурс, ознакомьтесь с разделом [Условное развертывание ресурса](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="e0921-105">If you need to add logic to your template that enables you to specify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="e0921-106">Итерация ресурса</span><span class="sxs-lookup"><span data-stu-id="e0921-106">Resource iteration</span></span>
<span data-ttu-id="e0921-107">Для создания нескольких экземпляров типа ресурса добавьте элемент `copy` к типу ресурса.</span><span class="sxs-lookup"><span data-stu-id="e0921-107">To create multiple instances of a resource type, add a `copy` element to the resource type.</span></span> <span data-ttu-id="e0921-108">В элементе копирования укажите число итераций и имя для этого цикла.</span><span class="sxs-lookup"><span data-stu-id="e0921-108">In the copy element, you specify the number of iterations and a name for this loop.</span></span> <span data-ttu-id="e0921-109">Значение count должно быть положительным целым числом не больше 800.</span><span class="sxs-lookup"><span data-stu-id="e0921-109">The count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="e0921-110">Resource Manager создает ресурсы параллельно.</span><span class="sxs-lookup"><span data-stu-id="e0921-110">Resource Manager creates the resources in parallel.</span></span> <span data-ttu-id="e0921-111">Поэтому порядок, в котором они создаются, не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="e0921-111">Therefore, the order in which they are created is not guaranteed.</span></span> <span data-ttu-id="e0921-112">Чтобы последовательно создать ресурсы с помощью итерации, ознакомьтесь с разделом [Последовательное копирование](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="e0921-112">To create iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="e0921-113">Для многократного создания ресурса используется следующий формат.</span><span class="sxs-lookup"><span data-stu-id="e0921-113">The resource to create multiple times takes the following format:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="e0921-114">Обратите внимание, что имя каждого ресурса содержит функцию `copyIndex()`, которая возвращает текущую итерацию в цикле.</span><span class="sxs-lookup"><span data-stu-id="e0921-114">Notice that the name of each resource includes the `copyIndex()` function, which returns the current iteration in the loop.</span></span> <span data-ttu-id="e0921-115">`copyIndex()` отсчитывается, начиная с нуля.</span><span class="sxs-lookup"><span data-stu-id="e0921-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="e0921-116">См. приведенный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="e0921-116">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="e0921-117">Он создает следующие имена:</span><span class="sxs-lookup"><span data-stu-id="e0921-117">Creates these names:</span></span>

* <span data-ttu-id="e0921-118">storage0;</span><span class="sxs-lookup"><span data-stu-id="e0921-118">storage0</span></span>
* <span data-ttu-id="e0921-119">storage1;</span><span class="sxs-lookup"><span data-stu-id="e0921-119">storage1</span></span>
* <span data-ttu-id="e0921-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="e0921-120">storage2.</span></span>

<span data-ttu-id="e0921-121">Чтобы сместить значение индекса, можно передать нужное значение в функцию copyIndex().</span><span class="sxs-lookup"><span data-stu-id="e0921-121">To offset the index value, you can pass a value in the copyIndex() function.</span></span> <span data-ttu-id="e0921-122">Число выполняемых итераций по-прежнему указывается в элементе копирования, но значение copyIndex сдвигается на указанное значение.</span><span class="sxs-lookup"><span data-stu-id="e0921-122">The number of iterations to perform is still specified in the copy element, but the value of copyIndex is offset by the specified value.</span></span> <span data-ttu-id="e0921-123">См. приведенный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="e0921-123">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="e0921-124">Он создает следующие имена:</span><span class="sxs-lookup"><span data-stu-id="e0921-124">Creates these names:</span></span>

* <span data-ttu-id="e0921-125">storage1;</span><span class="sxs-lookup"><span data-stu-id="e0921-125">storage1</span></span>
* <span data-ttu-id="e0921-126">storage2;</span><span class="sxs-lookup"><span data-stu-id="e0921-126">storage2</span></span>
* <span data-ttu-id="e0921-127">storage3.</span><span class="sxs-lookup"><span data-stu-id="e0921-127">storage3</span></span>

<span data-ttu-id="e0921-128">Операция копирования удобна при работе с массивами, так как позволяет выполнить итерацию по каждому элементу в массиве.</span><span class="sxs-lookup"><span data-stu-id="e0921-128">The copy operation is helpful when working with arrays because you can iterate through each element in the array.</span></span> <span data-ttu-id="e0921-129">Используйте функцию `length` в массиве, чтобы указать число итераций, а также функцию `copyIndex` для получения текущего индекса в массиве.</span><span class="sxs-lookup"><span data-stu-id="e0921-129">Use the `length` function on the array to specify the count for iterations, and `copyIndex` to retrieve the current index in the array.</span></span> <span data-ttu-id="e0921-130">См. приведенный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="e0921-130">So, the following example:</span></span>

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

<span data-ttu-id="e0921-131">Он создает следующие имена:</span><span class="sxs-lookup"><span data-stu-id="e0921-131">Creates these names:</span></span>

* <span data-ttu-id="e0921-132">storagecontoso;</span><span class="sxs-lookup"><span data-stu-id="e0921-132">storagecontoso</span></span>
* <span data-ttu-id="e0921-133">storagefabrikam;</span><span class="sxs-lookup"><span data-stu-id="e0921-133">storagefabrikam</span></span>
* <span data-ttu-id="e0921-134">storagecoho.</span><span class="sxs-lookup"><span data-stu-id="e0921-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="e0921-135">Последовательное копирование</span><span class="sxs-lookup"><span data-stu-id="e0921-135">Serial copy</span></span>

<span data-ttu-id="e0921-136">При использовании элемента copy для создания нескольких экземпляров типа ресурса по умолчанию Resource Manager развертывает эти экземпляры параллельно.</span><span class="sxs-lookup"><span data-stu-id="e0921-136">When you use the copy element to create multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="e0921-137">Тем не менее можно настроить последовательное развертывание ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e0921-137">However, you may want to specify that the resources are deployed in sequence.</span></span> <span data-ttu-id="e0921-138">Например, при обновлении рабочей среды может потребоваться дифференцировать обновления, чтобы только определенное число элементов могло быть обновлено в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="e0921-138">For example, when updating a production environment, you may want to stagger the updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="e0921-139">Resource Manager предоставляет свойства элемента copy, позволяющие последовательно развернуть несколько экземпляров.</span><span class="sxs-lookup"><span data-stu-id="e0921-139">Resource Manager provides properties on the copy element that enable you to serially deploy multiple instances.</span></span> <span data-ttu-id="e0921-140">В элементе copy задайте для `mode` значение **serial**, а для `batchSize` — число экземпляров, которые могут развертываться одновременно.</span><span class="sxs-lookup"><span data-stu-id="e0921-140">In the copy element, set `mode` to **serial** and `batchSize` to the number of instances to deploy at a time.</span></span> <span data-ttu-id="e0921-141">В последовательном режиме Resource Manager создает зависимость от предыдущих экземпляров в цикле, поэтому он не начинает выполнение следующего пакета до завершения предыдущего.</span><span class="sxs-lookup"><span data-stu-id="e0921-141">With serial mode, Resource Manager creates a dependency on earlier instances in the loop, so it does not start one batch until the previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="e0921-142">Свойство mode также принимает значение **parallel**, которое является значением по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e0921-142">The mode property also accepts **parallel**, which is the default value.</span></span>

<span data-ttu-id="e0921-143">Чтобы проверить последовательное копирование без создания фактических ресурсов, используйте следующий шаблон, который развертывает пустые вложенные шаблоны.</span><span class="sxs-lookup"><span data-stu-id="e0921-143">To test serial copy without creating actual resources, use the following template that deploys empty nested templates:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

<span data-ttu-id="e0921-144">В журнале развертывания обратите внимание на то, что вложенные развертывания обрабатываются последовательно.</span><span class="sxs-lookup"><span data-stu-id="e0921-144">In the deployment history, notice that the nested deployments are processed in sequence.</span></span>

![Последовательное развертывание](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="e0921-146">В качестве более реалистичного сценария приведен следующий пример. Он одновременно развертывает два экземпляра виртуальной машины Linux из вложенного шаблона.</span><span class="sxs-lookup"><span data-stu-id="e0921-146">For a more realistic scenario, the following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for the Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for the Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for the Public IP used to access the Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a><span data-ttu-id="e0921-147">Итерация свойства</span><span class="sxs-lookup"><span data-stu-id="e0921-147">Property iteration</span></span>

<span data-ttu-id="e0921-148">Чтобы создать несколько значений для свойства ресурса, добавьте массив `copy` в элемент properties.</span><span class="sxs-lookup"><span data-stu-id="e0921-148">To create multiple values for a property on a resource, add a `copy` array in the properties element.</span></span> <span data-ttu-id="e0921-149">Этот массив содержит объекты, каждый из которых имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="e0921-149">This array contains objects, and each object has the following properties:</span></span>

* <span data-ttu-id="e0921-150">name — имя свойства, для которого необходимо создать нескольких значений;</span><span class="sxs-lookup"><span data-stu-id="e0921-150">name - the name of the property to create multiple values for</span></span>
* <span data-ttu-id="e0921-151">count — количество значений, которые необходимо создать;</span><span class="sxs-lookup"><span data-stu-id="e0921-151">count - the number of values to create</span></span>
* <span data-ttu-id="e0921-152">input — объект, содержащий значения для назначения свойству.</span><span class="sxs-lookup"><span data-stu-id="e0921-152">input - an object that contains the values to assign to the property</span></span>  

<span data-ttu-id="e0921-153">В следующем примере показано, как применить массив `copy` к свойству dataDisks на виртуальной машине:</span><span class="sxs-lookup"><span data-stu-id="e0921-153">The following example shows how to apply `copy` to the dataDisks property on a virtual machine:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="e0921-154">Обратите внимание, что при использовании `copyIndex` в итерации свойства, необходимо указать имя итерации.</span><span class="sxs-lookup"><span data-stu-id="e0921-154">Notice that when using `copyIndex` inside a property iteration, you must provide the name of the iteration.</span></span> <span data-ttu-id="e0921-155">Вам не нужно указывать имя при использовании итерации ресурса.</span><span class="sxs-lookup"><span data-stu-id="e0921-155">You do not have to provide the name when used with resource iteration.</span></span>

<span data-ttu-id="e0921-156">Диспетчер ресурсов разворачивает массив `copy` во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="e0921-156">Resource Manager expands the `copy` array during deployment.</span></span> <span data-ttu-id="e0921-157">Имя массива становится именем свойства.</span><span class="sxs-lookup"><span data-stu-id="e0921-157">The name of the array becomes the name of the property.</span></span> <span data-ttu-id="e0921-158">Входные значения становятся свойствами объекта.</span><span class="sxs-lookup"><span data-stu-id="e0921-158">The input values become the object properties.</span></span> <span data-ttu-id="e0921-159">Развернутый шаблон выглядит так:</span><span class="sxs-lookup"><span data-stu-id="e0921-159">The deployed template becomes:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="e0921-160">Вы можете совместно использовать итерацию свойства и ресурса.</span><span class="sxs-lookup"><span data-stu-id="e0921-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="e0921-161">Обращайтесь к итерации свойства по имени.</span><span class="sxs-lookup"><span data-stu-id="e0921-161">Reference the property iteration by name.</span></span>

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

<span data-ttu-id="e0921-162">Вы можете включить только один элемент copy в properties для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="e0921-162">You can only include one copy element in the properties for each resource.</span></span> <span data-ttu-id="e0921-163">Чтобы указать цикл итерации для нескольких свойств, определите несколько объектов в массиве copy.</span><span class="sxs-lookup"><span data-stu-id="e0921-163">To specify an iteration loop for more than one property, define multiple objects in the copy array.</span></span> <span data-ttu-id="e0921-164">Итерация каждого объекта выполняется отдельно.</span><span class="sxs-lookup"><span data-stu-id="e0921-164">Each object is iterated separately.</span></span> <span data-ttu-id="e0921-165">Например, чтобы создать несколько экземпляров свойств `frontendIPConfigurations` и `loadBalancingRules` в балансировщике нагрузки, определите оба объекта в одном элементе copy:</span><span class="sxs-lookup"><span data-stu-id="e0921-165">For example, to create multiple instances of both the `frontendIPConfigurations` property and the `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="e0921-166">Зависимость от ресурсов в цикле</span><span class="sxs-lookup"><span data-stu-id="e0921-166">Depend on resources in a loop</span></span>
<span data-ttu-id="e0921-167">С помощью элемента `dependsOn` можно определить последовательность развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e0921-167">You specify that a resource is deployed after another resource by using the `dependsOn` element.</span></span> <span data-ttu-id="e0921-168">Чтобы развернуть ресурс, который зависит от коллекции ресурсов в цикле, укажите имя цикла копирования в элементе dependsOn.</span><span class="sxs-lookup"><span data-stu-id="e0921-168">To deploy a resource that depends on the collection of resources in a loop, provide the name of the copy loop in the dependsOn element.</span></span> <span data-ttu-id="e0921-169">В следующем примере показано, как развернуть три учетные записи хранения до развертывания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e0921-169">The following example shows how to deploy three storage accounts before deploying the Virtual Machine.</span></span> <span data-ttu-id="e0921-170">Полное определение виртуальной машины не показано.</span><span class="sxs-lookup"><span data-stu-id="e0921-170">The full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="e0921-171">Обратите внимание, что параметр name элемента copy имеет значение `storagecopy`, а элемент dependsOn для виртуальных машин имеет значение `storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="e0921-171">Notice that the copy element has name set to `storagecopy` and the dependsOn element for the Virtual Machines is also set to `storagecopy`.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="e0921-172">Создание нескольких экземпляров дочернего ресурса</span><span class="sxs-lookup"><span data-stu-id="e0921-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="e0921-173">Нельзя включить дочерний ресурс в цикл копирования.</span><span class="sxs-lookup"><span data-stu-id="e0921-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="e0921-174">Чтобы создать несколько экземпляров ресурса, которые определяются как вложенные в другой ресурс, необходимо создать его как ресурс верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="e0921-174">To create multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="e0921-175">Вы можете определить связь с родительским ресурсом с помощью свойств type и name.</span><span class="sxs-lookup"><span data-stu-id="e0921-175">You define the relationship with the parent resource through the type and name properties.</span></span>

<span data-ttu-id="e0921-176">Предположим, вы определяете набор данных как дочерний ресурс фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="e0921-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

<span data-ttu-id="e0921-177">Чтобы создать несколько экземпляров набора данных, переместите его за пределы фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="e0921-177">To create multiple instances of data sets, move it outside of the data factory.</span></span> <span data-ttu-id="e0921-178">Набор данных должен находиться на том же уровне, что и фабрика данных, но при этом он должен быть дочерним ресурсом фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="e0921-178">The dataset must be at the same level as the data factory, but it is still a child resource of the data factory.</span></span> <span data-ttu-id="e0921-179">Вы можете сохранить связь между набором данных и фабрикой данных с помощью свойств type и name.</span><span class="sxs-lookup"><span data-stu-id="e0921-179">You preserve the relationship between data set and data factory through the type and name properties.</span></span> <span data-ttu-id="e0921-180">Так как тип нельзя определить по положению в шаблоне, укажите полное имя типа в следующем формате: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="e0921-180">Since type can no longer be inferred from its position in the template, you must provide the fully qualified type in the format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="e0921-181">Чтобы установить связь между родительским и дочерним ресурсами, укажите имя набора данных, которое включает имя родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="e0921-181">To establish a parent/child relationship with an instance of the data factory, provide a name for the data set that includes the parent resource name.</span></span> <span data-ttu-id="e0921-182">Используйте формат `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="e0921-182">Use the format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="e0921-183">В следующем примере показано, как это сделать:</span><span class="sxs-lookup"><span data-stu-id="e0921-183">The following example shows the implementation:</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="e0921-184">Условное развертывание ресурса</span><span class="sxs-lookup"><span data-stu-id="e0921-184">Conditionally deploy resource</span></span>

<span data-ttu-id="e0921-185">Чтобы указать, развернут ли ресурс, используйте элемент `condition`.</span><span class="sxs-lookup"><span data-stu-id="e0921-185">To specify whether a resource is deployed, use the `condition` element.</span></span> <span data-ttu-id="e0921-186">Этот элемент возвращает значение True или False.</span><span class="sxs-lookup"><span data-stu-id="e0921-186">The value for this element resolves to true or false.</span></span> <span data-ttu-id="e0921-187">Если значение True, ресурс развернут.</span><span class="sxs-lookup"><span data-stu-id="e0921-187">When the value is true, the resource is deployed.</span></span> <span data-ttu-id="e0921-188">А если False — то не развернут.</span><span class="sxs-lookup"><span data-stu-id="e0921-188">When the value is false, the resource is not deployed.</span></span> <span data-ttu-id="e0921-189">Например, чтобы указать, развернута ли новая учетная запись хранения или используется ли имеющаяся, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e0921-189">For example, to specify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="e0921-190">Пример использования нового или имеющегося шаблона условий см. [здесь](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="e0921-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="e0921-191">Пример использования пароля или ключа SSH для развертывания виртуальной машины см. в [шаблоне имени пользователя или условия SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="e0921-191">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0921-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0921-192">Next steps</span></span>
* <span data-ttu-id="e0921-193">Сведения о разделах шаблона см. в статье, посвященной [созданию шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e0921-193">If you want to learn about the sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e0921-194">Инструкции по развертыванию шаблонов см. в статье, посвященной [развертыванию приложения с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e0921-194">To learn how to deploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

