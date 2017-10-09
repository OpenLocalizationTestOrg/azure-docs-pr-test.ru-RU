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
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Функции развертывания для шаблонов Azure Resource Manager 

Диспетчер ресурсов предоставляет hello следующие функции для получения значения из разделов шаблона hello и значения связанных toohello развертывания:

* [deployment](#deployment)
* [parameters](#parameters)
* [variables](#variables)

tooget значения из ресурсов, групп ресурсов или подписки, в разделе [функций ресурсов](resource-group-template-functions-resource.md).

<a id="deployment" />

## <a name="deployment"></a>Развертывание
`deployment()`

Возвращает сведения о текущей операции развертывания hello.

### <a name="return-value"></a>Возвращаемое значение

Эта функция возвращает hello объекта, передаваемого во время развертывания. свойства Hello в hello, возвращенный объект зависят от ли hello объекта развертывания передается как ссылка или как объект в строку. Hello объекта развертывания — при передаче в строки, например, при использовании hello **- TemplateFile** параметр в Azure PowerShell toopoint tooa локального файла, hello возвращается объект имеет hello следующий формат:

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

Когда hello объекта передается в качестве ссылки, например, когда с помощью hello **- TemplateUri** параметр toopoint tooa удаленного объекта hello объекта возвращается в hello следующий формат: 

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

### <a name="remarks"></a>Примечания

Можно использовать deployment() toolink tooanother шаблона, основанного на hello URI hello родительского шаблона.

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>Пример

Hello следующий пример возвращает hello объекта развертывания.

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

Hello выше пример возвращает hello следующих объектов:

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

## <a name="parameters"></a>parameters
`parameters(parameterName)`

Возвращает значение параметра. Hello указанное имя параметра должен быть определен в разделе параметров hello hello шаблона.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| имя_параметра |Да |string |Имя параметра tooreturn hello Hello. |

### <a name="return-value"></a>Возвращаемое значение

параметра указано значение Hello hello.

### <a name="remarks"></a>Примечания

Обычно используются значения ресурсов tooset параметров. Hello следующем примере задается имя hello значение параметра toohello веб-узла, переданного во время развертывания.

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

### <a name="example"></a>Пример

Hello пример упрощенного используйте параметры функции hello.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| stringOutput | Строка | вариант 1 |
| intOutput | int | 1 |
| objectOutput | Объект | {"one": "a", "two": "b"} |
| arrayOutput | Массив, | [1, 2, 3] |
| crossOutput | Строка | вариант 1 |

<a id="variables" />

## <a name="variables"></a>variables
`variables(variableName)`

Возвращает hello значение переменной. Указанное имя переменной Hello должен быть определен в разделе переменные hello hello шаблона.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| variableName |Да |Строка |Имя переменной tooreturn hello Hello. |

### <a name="return-value"></a>Возвращаемое значение

значение указанной переменной hello Hello.

### <a name="remarks"></a>Примечания

Обычно используется toosimplify переменных шаблона, создав сложных значений только один раз. Hello следующий пример создает уникальное имя для учетной записи хранилища.

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

### <a name="example"></a>Пример

Пример шаблона Hello возвращает разные значения переменной.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| exampleOutput1 | Строка | myVariable |
| exampleOutput2 | Массив, | [1, 2, 3, 4] |
| exampleOutput3 | Строка | myVariable |
| exampleOutput4 |  Объект | {"property1": "value1", "property2": "value2"} |

## <a name="next-steps"></a>Дальнейшие действия
* Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).
* tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).
* toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).

