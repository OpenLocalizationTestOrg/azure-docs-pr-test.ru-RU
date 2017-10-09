---
title: "aaaDeploy нескольких экземпляров ресурсов Azure | Документы Microsoft"
description: "Используйте операции копирования и массивов в tooiterate шаблона диспетчера ресурсов Azure несколько раз при развертывании ресурсов."
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
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="b42c9-103">Развертывание нескольких экземпляров ресурса или свойства в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b42c9-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="b42c9-104">В этом разделе показано, как tooiterate в вашей toocreate шаблона диспетчера ресурсов Azure несколько экземпляров ресурс или несколько экземпляров свойства ресурса.</span><span class="sxs-lookup"><span data-stu-id="b42c9-104">This topic shows you how tooiterate in your Azure Resource Manager template toocreate multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="b42c9-105">Если вам требуется tooadd логику tooyour шаблон, который позволяет toospecify развернут ли ресурс см. в разделе [условно развертывания ресурсов](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="b42c9-105">If you need tooadd logic tooyour template that enables you toospecify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="b42c9-106">Итерация ресурса</span><span class="sxs-lookup"><span data-stu-id="b42c9-106">Resource iteration</span></span>
<span data-ttu-id="b42c9-107">добавить несколько экземпляров типа ресурса toocreate `copy` тип ресурса toohello элемента.</span><span class="sxs-lookup"><span data-stu-id="b42c9-107">toocreate multiple instances of a resource type, add a `copy` element toohello resource type.</span></span> <span data-ttu-id="b42c9-108">В элементе копирования hello укажите hello количество итераций и имя для этого цикла.</span><span class="sxs-lookup"><span data-stu-id="b42c9-108">In hello copy element, you specify hello number of iterations and a name for this loop.</span></span> <span data-ttu-id="b42c9-109">значение count Hello должно быть положительным целым числом и не может превышать 800.</span><span class="sxs-lookup"><span data-stu-id="b42c9-109">hello count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="b42c9-110">Диспетчер ресурсов создает ресурсы hello в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="b42c9-110">Resource Manager creates hello resources in parallel.</span></span> <span data-ttu-id="b42c9-111">Hello порядок, в котором они были созданы не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="b42c9-111">Therefore, hello order in which they are created is not guaranteed.</span></span> <span data-ttu-id="b42c9-112">Итерация toocreate ресурсы в последовательности, в разделе [последовательного копирования](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="b42c9-112">toocreate iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="b42c9-113">Hello ресурсов toocreate несколько раз принимает hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="b42c9-113">hello resource toocreate multiple times takes hello following format:</span></span>

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

<span data-ttu-id="b42c9-114">Обратите внимание, что hello имя каждого ресурса содержит hello `copyIndex()` функция, возвращающая hello текущей итерации цикла hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-114">Notice that hello name of each resource includes hello `copyIndex()` function, which returns hello current iteration in hello loop.</span></span> <span data-ttu-id="b42c9-115">`copyIndex()` отсчитывается, начиная с нуля.</span><span class="sxs-lookup"><span data-stu-id="b42c9-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="b42c9-116">Следующий пример в этом случае hello:</span><span class="sxs-lookup"><span data-stu-id="b42c9-116">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="b42c9-117">Он создает следующие имена:</span><span class="sxs-lookup"><span data-stu-id="b42c9-117">Creates these names:</span></span>

* <span data-ttu-id="b42c9-118">storage0;</span><span class="sxs-lookup"><span data-stu-id="b42c9-118">storage0</span></span>
* <span data-ttu-id="b42c9-119">storage1;</span><span class="sxs-lookup"><span data-stu-id="b42c9-119">storage1</span></span>
* <span data-ttu-id="b42c9-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="b42c9-120">storage2.</span></span>

<span data-ttu-id="b42c9-121">значение индекса toooffset hello, можно передать значение в функции copyIndex() hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-121">toooffset hello index value, you can pass a value in hello copyIndex() function.</span></span> <span data-ttu-id="b42c9-122">Hello количество итераций tooperform по-прежнему указывается в элемента copy hello, но значение hello copyIndex смещением hello указано значение.</span><span class="sxs-lookup"><span data-stu-id="b42c9-122">hello number of iterations tooperform is still specified in hello copy element, but hello value of copyIndex is offset by hello specified value.</span></span> <span data-ttu-id="b42c9-123">Следующий пример в этом случае hello:</span><span class="sxs-lookup"><span data-stu-id="b42c9-123">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="b42c9-124">Он создает следующие имена:</span><span class="sxs-lookup"><span data-stu-id="b42c9-124">Creates these names:</span></span>

* <span data-ttu-id="b42c9-125">storage1;</span><span class="sxs-lookup"><span data-stu-id="b42c9-125">storage1</span></span>
* <span data-ttu-id="b42c9-126">storage2;</span><span class="sxs-lookup"><span data-stu-id="b42c9-126">storage2</span></span>
* <span data-ttu-id="b42c9-127">storage3.</span><span class="sxs-lookup"><span data-stu-id="b42c9-127">storage3</span></span>

<span data-ttu-id="b42c9-128">Операция копирования Hello полезно при работе с массивами, так как каждый элемент массива hello итерацию.</span><span class="sxs-lookup"><span data-stu-id="b42c9-128">hello copy operation is helpful when working with arrays because you can iterate through each element in hello array.</span></span> <span data-ttu-id="b42c9-129">Используйте hello `length` функции hello массива toospecify hello число итераций, и `copyIndex` tooretrieve hello текущий индекс в массиве hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-129">Use hello `length` function on hello array toospecify hello count for iterations, and `copyIndex` tooretrieve hello current index in hello array.</span></span> <span data-ttu-id="b42c9-130">Следующий пример в этом случае hello:</span><span class="sxs-lookup"><span data-stu-id="b42c9-130">So, hello following example:</span></span>

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

<span data-ttu-id="b42c9-131">Он создает следующие имена:</span><span class="sxs-lookup"><span data-stu-id="b42c9-131">Creates these names:</span></span>

* <span data-ttu-id="b42c9-132">storagecontoso;</span><span class="sxs-lookup"><span data-stu-id="b42c9-132">storagecontoso</span></span>
* <span data-ttu-id="b42c9-133">storagefabrikam;</span><span class="sxs-lookup"><span data-stu-id="b42c9-133">storagefabrikam</span></span>
* <span data-ttu-id="b42c9-134">storagecoho.</span><span class="sxs-lookup"><span data-stu-id="b42c9-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="b42c9-135">Последовательное копирование</span><span class="sxs-lookup"><span data-stu-id="b42c9-135">Serial copy</span></span>

<span data-ttu-id="b42c9-136">При использовании hello Копировать элемент toocreate несколько экземпляров типа ресурса, диспетчер ресурсов по умолчанию развертывает эти экземпляры в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="b42c9-136">When you use hello copy element toocreate multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="b42c9-137">Тем не менее вы можете toospecify, hello ресурсы развертываются в последовательности.</span><span class="sxs-lookup"><span data-stu-id="b42c9-137">However, you may want toospecify that hello resources are deployed in sequence.</span></span> <span data-ttu-id="b42c9-138">Например, при обновлении рабочей среде, можно toostagger hello обновляет только определенное число обновляются в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="b42c9-138">For example, when updating a production environment, you may want toostagger hello updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="b42c9-139">Диспетчер ресурсов предоставляет свойства для копирования элемента hello, которые позволяют вам tooserially развертывание нескольких экземпляров.</span><span class="sxs-lookup"><span data-stu-id="b42c9-139">Resource Manager provides properties on hello copy element that enable you tooserially deploy multiple instances.</span></span> <span data-ttu-id="b42c9-140">В набор элементов для копирования hello, `mode` слишком**последовательной** и `batchSize` toohello число экземпляров toodeploy одновременно.</span><span class="sxs-lookup"><span data-stu-id="b42c9-140">In hello copy element, set `mode` too**serial** and `batchSize` toohello number of instances toodeploy at a time.</span></span> <span data-ttu-id="b42c9-141">С помощью последовательного режима диспетчера ресурсов создает зависимость от предыдущих экземпляров в цикле hello, один пакет не запускаются до завершения предыдущего пакета hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-141">With serial mode, Resource Manager creates a dependency on earlier instances in hello loop, so it does not start one batch until hello previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="b42c9-142">Hello свойство режима также принимает **параллельных**, которое является значением по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-142">hello mode property also accepts **parallel**, which is hello default value.</span></span>

<span data-ttu-id="b42c9-143">tootest последовательного копирования без создания фактические ресурсы hello используйте следующий шаблон, который развертывает пустые вложенные шаблоны:</span><span class="sxs-lookup"><span data-stu-id="b42c9-143">tootest serial copy without creating actual resources, use hello following template that deploys empty nested templates:</span></span>

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

<span data-ttu-id="b42c9-144">В журнале развертывания hello Обратите внимание, что hello вложенных развертываний, обрабатываются последовательно.</span><span class="sxs-lookup"><span data-stu-id="b42c9-144">In hello deployment history, notice that hello nested deployments are processed in sequence.</span></span>

![Последовательное развертывание](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="b42c9-146">Для более реалистичном случае следующий пример hello развертывает два экземпляра во время из вложенного шаблона виртуальной машины Linux:</span><span class="sxs-lookup"><span data-stu-id="b42c9-146">For a more realistic scenario, hello following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
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
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
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

## <a name="property-iteration"></a><span data-ttu-id="b42c9-147">Итерация свойства</span><span class="sxs-lookup"><span data-stu-id="b42c9-147">Property iteration</span></span>

<span data-ttu-id="b42c9-148">добавить несколько значений для свойства ресурса, toocreate `copy` массива в элементе свойства hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-148">toocreate multiple values for a property on a resource, add a `copy` array in hello properties element.</span></span> <span data-ttu-id="b42c9-149">Этот массив содержит объекты, и каждый объект имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="b42c9-149">This array contains objects, and each object has hello following properties:</span></span>

* <span data-ttu-id="b42c9-150">имя — имя hello объекта toocreate свойство hello несколько значений для</span><span class="sxs-lookup"><span data-stu-id="b42c9-150">name - hello name of hello property toocreate multiple values for</span></span>
* <span data-ttu-id="b42c9-151">число — количество hello toocreate значения</span><span class="sxs-lookup"><span data-stu-id="b42c9-151">count - hello number of values toocreate</span></span>
* <span data-ttu-id="b42c9-152">входные данные — это объект, содержащий tooassign toohello hello значения свойства</span><span class="sxs-lookup"><span data-stu-id="b42c9-152">input - an object that contains hello values tooassign toohello property</span></span>  

<span data-ttu-id="b42c9-153">Следующий пример показывает как Hello tooapply `copy` toohello dataDisks свойства на виртуальной машине:</span><span class="sxs-lookup"><span data-stu-id="b42c9-153">hello following example shows how tooapply `copy` toohello dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="b42c9-154">Обратите внимание, что при использовании `copyIndex` внутри свойства итерации, необходимо указать имя hello hello итерации.</span><span class="sxs-lookup"><span data-stu-id="b42c9-154">Notice that when using `copyIndex` inside a property iteration, you must provide hello name of hello iteration.</span></span> <span data-ttu-id="b42c9-155">У вас имя hello tooprovide при использовании ресурсов итерации.</span><span class="sxs-lookup"><span data-stu-id="b42c9-155">You do not have tooprovide hello name when used with resource iteration.</span></span>

<span data-ttu-id="b42c9-156">Диспетчер ресурсов расширяет hello `copy` массива во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="b42c9-156">Resource Manager expands hello `copy` array during deployment.</span></span> <span data-ttu-id="b42c9-157">Имя Hello массива hello становится именем hello hello свойства.</span><span class="sxs-lookup"><span data-stu-id="b42c9-157">hello name of hello array becomes hello name of hello property.</span></span> <span data-ttu-id="b42c9-158">входные значения Hello становятся hello объекта свойства.</span><span class="sxs-lookup"><span data-stu-id="b42c9-158">hello input values become hello object properties.</span></span> <span data-ttu-id="b42c9-159">Шаблон развертывания Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b42c9-159">hello deployed template becomes:</span></span>

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

<span data-ttu-id="b42c9-160">Вы можете совместно использовать итерацию свойства и ресурса.</span><span class="sxs-lookup"><span data-stu-id="b42c9-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="b42c9-161">Справочник по итерации hello свойства по имени.</span><span class="sxs-lookup"><span data-stu-id="b42c9-161">Reference hello property iteration by name.</span></span>

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

<span data-ttu-id="b42c9-162">В свойствах hello для каждого ресурса может содержать только один элемент для копирования.</span><span class="sxs-lookup"><span data-stu-id="b42c9-162">You can only include one copy element in hello properties for each resource.</span></span> <span data-ttu-id="b42c9-163">toospecify итерации цикла для более чем одного свойства определить несколько объектов в массиве копирования hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-163">toospecify an iteration loop for more than one property, define multiple objects in hello copy array.</span></span> <span data-ttu-id="b42c9-164">Итерация каждого объекта выполняется отдельно.</span><span class="sxs-lookup"><span data-stu-id="b42c9-164">Each object is iterated separately.</span></span> <span data-ttu-id="b42c9-165">Например, toocreate несколько экземпляров обоих hello `frontendIPConfigurations` свойство и hello `loadBalancingRules` свойство в подсистеме балансировки нагрузки определять оба объекта в элементе одной копии:</span><span class="sxs-lookup"><span data-stu-id="b42c9-165">For example, toocreate multiple instances of both hello `frontendIPConfigurations` property and hello `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

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

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="b42c9-166">Зависимость от ресурсов в цикле</span><span class="sxs-lookup"><span data-stu-id="b42c9-166">Depend on resources in a loop</span></span>
<span data-ttu-id="b42c9-167">Укажите, что ресурс развернут после другой ресурс с помощью hello `dependsOn` элемента.</span><span class="sxs-lookup"><span data-stu-id="b42c9-167">You specify that a resource is deployed after another resource by using hello `dependsOn` element.</span></span> <span data-ttu-id="b42c9-168">toodeploy ресурс, который зависит от hello коллекцию ресурсов в цикле, укажите имя hello копирования цикла hello элемент dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-168">toodeploy a resource that depends on hello collection of resources in a loop, provide hello name of hello copy loop in hello dependsOn element.</span></span> <span data-ttu-id="b42c9-169">Hello в следующем примере показано, как toodeploy три учетные записи хранения перед развертыванием hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b42c9-169">hello following example shows how toodeploy three storage accounts before deploying hello Virtual Machine.</span></span> <span data-ttu-id="b42c9-170">полное определение виртуальной машины Hello не указывается.</span><span class="sxs-lookup"><span data-stu-id="b42c9-170">hello full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="b42c9-171">Обратите внимание на то этого элемента copy hello имя задано слишком`storagecopy` и элемент dependsOn hello для hello виртуальные машины также имеет слишком`storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="b42c9-171">Notice that hello copy element has name set too`storagecopy` and hello dependsOn element for hello Virtual Machines is also set too`storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="b42c9-172">Создание нескольких экземпляров дочернего ресурса</span><span class="sxs-lookup"><span data-stu-id="b42c9-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="b42c9-173">Нельзя включить дочерний ресурс в цикл копирования.</span><span class="sxs-lookup"><span data-stu-id="b42c9-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="b42c9-174">toocreate несколько экземпляров ресурса, который обычно определяется как вложенный в другой ресурс, необходимо вместо этого создать этот ресурс как ресурс верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="b42c9-174">toocreate multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="b42c9-175">Можно определить hello связь с родительского ресурса hello через hello тип и имя свойства.</span><span class="sxs-lookup"><span data-stu-id="b42c9-175">You define hello relationship with hello parent resource through hello type and name properties.</span></span>

<span data-ttu-id="b42c9-176">Предположим, вы определяете набор данных как дочерний ресурс фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="b42c9-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="b42c9-177">toocreate несколько экземпляров наборов данных, переместите его вне фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-177">toocreate multiple instances of data sets, move it outside of hello data factory.</span></span> <span data-ttu-id="b42c9-178">Hello набор данных должен быть hello же уровня как hello фабрики данных, но она по-прежнему дочерний ресурс hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="b42c9-178">hello dataset must be at hello same level as hello data factory, but it is still a child resource of hello data factory.</span></span> <span data-ttu-id="b42c9-179">Можно сохранить hello связь между набора данных и фабрику данных через hello тип и имя свойства.</span><span class="sxs-lookup"><span data-stu-id="b42c9-179">You preserve hello relationship between data set and data factory through hello type and name properties.</span></span> <span data-ttu-id="b42c9-180">Так как тип не может быть выведен из его положение в шаблоне hello, необходимо указать тип полное hello в формате hello: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="b42c9-180">Since type can no longer be inferred from its position in hello template, you must provide hello fully qualified type in hello format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="b42c9-181">tooestablish иерархическое отношение с экземпляром hello фабрики данных, введите имя для набора данных hello, которая включает имя родительского ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-181">tooestablish a parent/child relationship with an instance of hello data factory, provide a name for hello data set that includes hello parent resource name.</span></span> <span data-ttu-id="b42c9-182">Использование формата hello: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="b42c9-182">Use hello format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="b42c9-183">Hello ниже приведен пример реализации hello.</span><span class="sxs-lookup"><span data-stu-id="b42c9-183">hello following example shows hello implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="b42c9-184">Условное развертывание ресурса</span><span class="sxs-lookup"><span data-stu-id="b42c9-184">Conditionally deploy resource</span></span>

<span data-ttu-id="b42c9-185">toospecify ли ресурс развернут, использовать hello `condition` элемента.</span><span class="sxs-lookup"><span data-stu-id="b42c9-185">toospecify whether a resource is deployed, use hello `condition` element.</span></span> <span data-ttu-id="b42c9-186">Hello значение для этого элемента разрешает tootrue или false.</span><span class="sxs-lookup"><span data-stu-id="b42c9-186">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="b42c9-187">Если hello значение равно true, ресурс hello развернут.</span><span class="sxs-lookup"><span data-stu-id="b42c9-187">When hello value is true, hello resource is deployed.</span></span> <span data-ttu-id="b42c9-188">Если hello значение равно false, ресурс hello не развернут.</span><span class="sxs-lookup"><span data-stu-id="b42c9-188">When hello value is false, hello resource is not deployed.</span></span> <span data-ttu-id="b42c9-189">Например toospecify ли развернуть новую учетную запись хранилища или использовать существующую учетную запись хранения, используйте:</span><span class="sxs-lookup"><span data-stu-id="b42c9-189">For example, toospecify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="b42c9-190">Пример использования нового или имеющегося шаблона условий см. [здесь](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="b42c9-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="b42c9-191">Пример использования пароля или SSH ключа toodeploy виртуальной машины, в разделе [имя пользователя или SSH условие шаблона](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="b42c9-191">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b42c9-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b42c9-192">Next steps</span></span>
* <span data-ttu-id="b42c9-193">Toolearn о разделах hello шаблона см [разработки шаблоны Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b42c9-193">If you want toolearn about hello sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="b42c9-194">toolearn как toodeploy шаблону, в разделе [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b42c9-194">toolearn how toodeploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

