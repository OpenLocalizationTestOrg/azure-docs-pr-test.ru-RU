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
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>Развертывание нескольких экземпляров ресурса или свойства в шаблонах Azure Resource Manager
В этом разделе показано, как tooiterate в вашей toocreate шаблона диспетчера ресурсов Azure несколько экземпляров ресурс или несколько экземпляров свойства ресурса.

Если вам требуется tooadd логику tooyour шаблон, который позволяет toospecify развернут ли ресурс см. в разделе [условно развертывания ресурсов](#conditionally-deploy-resource).

## <a name="resource-iteration"></a>Итерация ресурса
добавить несколько экземпляров типа ресурса toocreate `copy` тип ресурса toohello элемента. В элементе копирования hello укажите hello количество итераций и имя для этого цикла. значение count Hello должно быть положительным целым числом и не может превышать 800. Диспетчер ресурсов создает ресурсы hello в параллельном режиме. Hello порядок, в котором они были созданы не гарантируется. Итерация toocreate ресурсы в последовательности, в разделе [последовательного копирования](#serial-copy). 

Hello ресурсов toocreate несколько раз принимает hello следующий формат:

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

Обратите внимание, что hello имя каждого ресурса содержит hello `copyIndex()` функция, возвращающая hello текущей итерации цикла hello. `copyIndex()` отсчитывается, начиная с нуля. Следующий пример в этом случае hello:

```json
"name": "[concat('storage', copyIndex())]",
```

Он создает следующие имена:

* storage0;
* storage1;
* storage2.

значение индекса toooffset hello, можно передать значение в функции copyIndex() hello. Hello количество итераций tooperform по-прежнему указывается в элемента copy hello, но значение hello copyIndex смещением hello указано значение. Следующий пример в этом случае hello:

```json
"name": "[concat('storage', copyIndex(1))]",
```

Он создает следующие имена:

* storage1;
* storage2;
* storage3.

Операция копирования Hello полезно при работе с массивами, так как каждый элемент массива hello итерацию. Используйте hello `length` функции hello массива toospecify hello число итераций, и `copyIndex` tooretrieve hello текущий индекс в массиве hello. Следующий пример в этом случае hello:

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

Он создает следующие имена:

* storagecontoso;
* storagefabrikam;
* storagecoho.

## <a name="serial-copy"></a>Последовательное копирование

При использовании hello Копировать элемент toocreate несколько экземпляров типа ресурса, диспетчер ресурсов по умолчанию развертывает эти экземпляры в параллельном режиме. Тем не менее вы можете toospecify, hello ресурсы развертываются в последовательности. Например, при обновлении рабочей среде, можно toostagger hello обновляет только определенное число обновляются в любой момент времени.

Диспетчер ресурсов предоставляет свойства для копирования элемента hello, которые позволяют вам tooserially развертывание нескольких экземпляров. В набор элементов для копирования hello, `mode` слишком**последовательной** и `batchSize` toohello число экземпляров toodeploy одновременно. С помощью последовательного режима диспетчера ресурсов создает зависимость от предыдущих экземпляров в цикле hello, один пакет не запускаются до завершения предыдущего пакета hello.

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

Hello свойство режима также принимает **параллельных**, которое является значением по умолчанию hello.

tootest последовательного копирования без создания фактические ресурсы hello используйте следующий шаблон, который развертывает пустые вложенные шаблоны:

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

В журнале развертывания hello Обратите внимание, что hello вложенных развертываний, обрабатываются последовательно.

![Последовательное развертывание](./media/resource-group-create-multiple/serial-copy.png)

Для более реалистичном случае следующий пример hello развертывает два экземпляра во время из вложенного шаблона виртуальной машины Linux:

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

## <a name="property-iteration"></a>Итерация свойства

добавить несколько значений для свойства ресурса, toocreate `copy` массива в элементе свойства hello. Этот массив содержит объекты, и каждый объект имеет hello следующие свойства:

* имя — имя hello объекта toocreate свойство hello несколько значений для
* число — количество hello toocreate значения
* входные данные — это объект, содержащий tooassign toohello hello значения свойства  

Следующий пример показывает как Hello tooapply `copy` toohello dataDisks свойства на виртуальной машине:

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

Обратите внимание, что при использовании `copyIndex` внутри свойства итерации, необходимо указать имя hello hello итерации. У вас имя hello tooprovide при использовании ресурсов итерации.

Диспетчер ресурсов расширяет hello `copy` массива во время развертывания. Имя Hello массива hello становится именем hello hello свойства. входные значения Hello становятся hello объекта свойства. Шаблон развертывания Hello выглядит следующим образом:

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

Вы можете совместно использовать итерацию свойства и ресурса. Справочник по итерации hello свойства по имени.

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

В свойствах hello для каждого ресурса может содержать только один элемент для копирования. toospecify итерации цикла для более чем одного свойства определить несколько объектов в массиве копирования hello. Итерация каждого объекта выполняется отдельно. Например, toocreate несколько экземпляров обоих hello `frontendIPConfigurations` свойство и hello `loadBalancingRules` свойство в подсистеме балансировки нагрузки определять оба объекта в элементе одной копии: 

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

## <a name="depend-on-resources-in-a-loop"></a>Зависимость от ресурсов в цикле
Укажите, что ресурс развернут после другой ресурс с помощью hello `dependsOn` элемента. toodeploy ресурс, который зависит от hello коллекцию ресурсов в цикле, укажите имя hello копирования цикла hello элемент dependsOn hello. Hello в следующем примере показано, как toodeploy три учетные записи хранения перед развертыванием hello виртуальной машины. полное определение виртуальной машины Hello не указывается. Обратите внимание на то этого элемента copy hello имя задано слишком`storagecopy` и элемент dependsOn hello для hello виртуальные машины также имеет слишком`storagecopy`.

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

## <a name="create-multiple-instances-of-a-child-resource"></a>Создание нескольких экземпляров дочернего ресурса
Нельзя включить дочерний ресурс в цикл копирования. toocreate несколько экземпляров ресурса, который обычно определяется как вложенный в другой ресурс, необходимо вместо этого создать этот ресурс как ресурс верхнего уровня. Можно определить hello связь с родительского ресурса hello через hello тип и имя свойства.

Предположим, вы определяете набор данных как дочерний ресурс фабрики данных.

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

toocreate несколько экземпляров наборов данных, переместите его вне фабрики данных hello. Hello набор данных должен быть hello же уровня как hello фабрики данных, но она по-прежнему дочерний ресурс hello фабрики данных. Можно сохранить hello связь между набора данных и фабрику данных через hello тип и имя свойства. Так как тип не может быть выведен из его положение в шаблоне hello, необходимо указать тип полное hello в формате hello: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.

tooestablish иерархическое отношение с экземпляром hello фабрики данных, введите имя для набора данных hello, которая включает имя родительского ресурса hello. Использование формата hello: `{parent-resource-name}/{child-resource-name}`.  

Hello ниже приведен пример реализации hello.

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

## <a name="conditionally-deploy-resource"></a>Условное развертывание ресурса

toospecify ли ресурс развернут, использовать hello `condition` элемента. Hello значение для этого элемента разрешает tootrue или false. Если hello значение равно true, ресурс hello развернут. Если hello значение равно false, ресурс hello не развернут. Например toospecify ли развернуть новую учетную запись хранилища или использовать существующую учетную запись хранения, используйте:

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

Пример использования нового или имеющегося шаблона условий см. [здесь](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

Пример использования пароля или SSH ключа toodeploy виртуальной машины, в разделе [имя пользователя или SSH условие шаблона](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="next-steps"></a>Дальнейшие действия
* Toolearn о разделах hello шаблона см [разработки шаблоны Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn как toodeploy шаблону, в разделе [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).

