---
title: "Диспетчер ресурсов aaaAzure шаблона структуре и синтаксисе | Документы Microsoft"
description: "Описывает структуру hello и свойства с помощью декларативного синтаксиса JSON шаблонов диспетчера ресурсов Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a>Описание структуры hello и синтаксис шаблонов диспетчера ресурсов Azure
В этом разделе описывается структура hello шаблона диспетчера ресурсов Azure. Представляет различные разделы шаблона и hello свойства, которые доступны в этих разделах hello. шаблон Hello состоит из выражения, что tooconstruct значения можно использовать для развертывания и JSON. Пошаговое руководство по созданию шаблона приведено в разделе [Создание первого шаблона Azure Resource Manager](resource-manager-create-first-template.md).

## <a name="template-format"></a>Формат шаблона
В его Простейшая структура шаблона содержит hello следующие элементы:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| Имя элемента | Обязательно | Описание |
|:--- |:--- |:--- |
| $schema |Да |Расположение файла схемы JSON hello, описывающего версию hello hello шаблона языка. Используйте hello URL-адрес, показанный на предшествующий пример hello. |
| contentVersion |Да |Версия шаблона hello (например, 1.0.0.0). Для этого элемента можно предоставить любое значение. При развертывании ресурсов с помощью шаблона hello, это значение может быть используется toomake в том, что используется правильный шаблон, hello. |
| parameters |Нет |Значения, которые предоставляются при развертывании выполняются toocustomize развертывания ресурсов. |
| variables |Нет |Значения, которые используются в качестве фрагментов JSON в выражениях языка шаблона toosimplify шаблона hello. |
| ресурсов |Да |Типы ресурсов, которые развертываются или обновляются в группе ресурсов. |
| outputs |Нет |Значения, возвращаемые после развертывания. |

Каждый элемент содержит свойства, которые можно задать. Следующий пример Hello содержит hello полный синтаксис для шаблона:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

Мы изучаем hello разделах шаблона hello более подробно далее в этом разделе.

## <a name="expressions-and-functions"></a>Выражения и функции
Базовый синтаксис Hello hello шаблона является JSON. Однако выражения и функции расширить значений JSON hello, доступных в шаблоне hello.  Выражения записываются с помощью JSON строковые литералы, первого и последние символы являются скобкой hello: `[` и `]`соответственно. значение Hello hello выражения вычисляется при развертывании шаблона hello. Во время записи как строковый литерал hello результат вычисления выражения hello может быть другого типа JSON, например массиву или целое число, в зависимости от фактического выражение hello.  строковый литерал запустить скобкой toohave `[`, без его интерпретируются как выражения, добавляется строка hello toostart дополнительную квадратную скобку с `[[`.

Как правило используются выражения с помощью функции tooperform операций для настройки развертывания hello. Как и в языке JavaScript, вызовы функций форматируются так: `functionName(arg1,arg2,arg3)`. Ссылки на свойства с помощью операторов [index] и точками hello.

Hello в следующем примере показано, как toouse, некоторые функции при создании значения:

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Hello полный список функций шаблонов см. в разделе [функции шаблона Azure Resource Manager](resource-group-template-functions.md). 

## <a name="parameters"></a>Параметры
В разделе параметров hello шаблона hello укажите значения, которые можно ввести при развертывании hello ресурсы. Значения этих параметров включить toocustomize hello развертывания, предоставляя значения, которые предназначены для определенной среде (например, разработки, тестирования и эксплуатации). У вас tooprovide параметры в шаблоне, но без параметров ваш шаблон будет всегда следует развертывать hello и те же ресурсы с hello одинаковые имена, расположения и свойства.

Определить параметры с hello следующие структуры:

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| Имя элемента | Обязательно | Описание |
|:--- |:--- |:--- |
| имя_параметра |Да |Имя параметра hello. Должно быть допустимым идентификатором JavaScript. |
| type |Да |Тип значения параметра hello. После этой таблицы. в разделе hello списка разрешенных типов. |
| defaultValue |Нет |Значение по умолчанию для параметра hello, если значение не указано для параметра hello. |
| allowedValues |Нет |Массив допустимых значений для hello параметр toomake материалы hello правильного значения. |
| minValue |Нет |Hello минимальное значение для параметров типа int, это значение является включительно. |
| maxValue |Нет |Hello максимальное значение для параметров типа int, это значение равно включительно. |
| minLength |Нет |Hello минимальную длину строки, secureString и параметры типа массива, это значение является включительно. |
| maxLength |Нет |Hello Максимальная длина строки secureString и параметры типа массива, это значение является включительно. |
| Описание |Нет |Описание параметра hello, отображаться toousers через портал hello. |

Hello допустимые типы и значения являются:

* **string**
* **secureString**;
* **int**
* **bool**;
* **object**; 
* **secureObject**;
* **array**.

toospecify параметр как необязательный, укажите значение по умолчанию (может быть пустой строкой). 

При указании имени параметра в шаблон, соответствующий параметр в шаблон hello toodeploy hello команды нет возможной неоднозначности о заданные значения hello. Диспетчер ресурсов устраняет этой путаницы, добавив постфиксная hello **FromTemplate** toohello параметр шаблона. Например, если включить параметр с именем **ResourceGroupName** в шаблоне, это противоречит hello **ResourceGroupName** параметр в hello [ Новый AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) командлета. Во время развертывания, вы являетесь запрашиваемые tooprovide значение **ResourceGroupNameFromTemplate**. В общем случае следует избегать этой путаницы, не присвоив имена параметров с hello точно такое же имя в качестве параметров, используемых для операций развертывания.

> [!NOTE]
> Все пароли, ключи и другие секретные данные следует использовать hello **secureString** типа. При передаче конфиденциальных данных в объект JSON, следует использовать hello **secureObject** типа. Параметры шаблона с типами secureString и secureObject невозможно прочитать после развертывания ресурса. 
> 
> Например hello следующую запись в журнале развертывания hello показывает значение hello для string и object, но не для secureString и secureObject.
>
> ![показать значения развертывания](./media/resource-group-authoring-templates/show-parameters.png)  
>

Следующий пример показывает как Hello toodefine параметры:

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

Как значения параметров tooinput hello, во время развертывания, в разделе [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md). 

## <a name="variables"></a>Переменные
В разделе "переменные" hello создания значений, которые могут использоваться в шаблоне. Переменные toodefine не обязательно, но они часто упростить шаблон за счет уменьшения сложных выражений.

Определите переменные с hello следующие структуры:

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

Следующий пример показывает как Hello toodefine переменную, которая создается из значений двух параметров:

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

Hello далее пример переменной, которая является сложным типом, JSON и переменные, которые созданы из других переменных.

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a>Ресурсы
В разделе "ресурсы" hello необходимо указать hello ресурсы, которые будут развертываться или обновляться. В этом разделе может усложняться так, как необходимо понимать типы hello вы развертываете tooprovide hello правильные значения. Hello ресурсом значения (apiVersion, тип и свойства), необходимо tooset см [определения ресурсов в шаблоны Azure Resource Manager](/azure/templates/). 

Определить ресурсы с hello следующие структуры:

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| Имя элемента | Обязательно | Описание |
|:--- |:--- |:--- |
| condition | Нет | Логическое значение, указывающее, развернуто ли ресурс hello. |
| версия_API |Да |Версия toouse hello API-интерфейса REST для создания ресурсов hello. |
| type |Да |Тип ресурса hello. Это значение представляет собой сочетание hello пространство имен поставщика ресурсов hello и тип ресурса hello (такие как **Microsoft.Storage/storageAccounts**). |
| name |Да |Имя ресурса hello. Hello имя должно соответствовать ограничениям для компонента URI определен в RFC3986. Кроме того, Azure службы, предоставляющие имя toooutside hello ресурсов сторон проверки убедитесь, что не toospoof попытка toomake имя hello другим удостоверением. |
| location |Varies |Поддерживаемые географические расположения hello существовало ресурсов. Можно выбрать любой из доступных расположений hello, но обычно он выполняет toopick смысле это закрыть tooyour пользователей. Как правило, также имеет смысл tooplace ресурсы, которые взаимодействуют друг с другом в hello же области. Большинству типов ресурсов нужно расположение, но некоторым типам (например, назначению роли) оно не требуется. Ознакомьтесь с разделом [Определение расположения ресурса в шаблонах Azure Resource Manager](resource-manager-template-location.md). |
| tags |Нет |Теги, связанные с ресурсом hello. Ознакомьтесь с разделом [Присвоение тегов ресурсам в шаблоне Azure Resource Manager](resource-manager-template-tags.md). |
| комментарии |Нет |Заметки для документирования hello ресурсы в шаблон |
| копирование |Нет |Если требуется более одного экземпляра hello число toocreate ресурсов. режим по умолчанию Hello работает параллельно. Укажите режим последовательного hello toodeploy ресурсы в hello или не все одновременно. Дополнительные сведения см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md). |
| Свойство dependsOn |Нет |Ресурсы, которые должны быть развернуты перед развертыванием этого ресурса. Диспетчер ресурсов оценивает hello зависимости между ресурсами и развертывает их в правильном порядке hello. Если ресурсы не зависят друг от друга, они развертываются параллельно. Hello значение может быть ресурса список разделенных запятыми имен или уникальные идентификаторы ресурса. Выводится только список ресурсов, развертываемых в этом шаблоне. Ресурсы, которые не определены в этом шаблоне, уже должны существовать. Избегайте добавления ненужных зависимостей, так как это может замедлить развертывание и привести к созданию циклических зависимостей. Рекомендации по настройке зависимостей см. в статье [Определение зависимостей в шаблонах диспетчера ресурсов Azure](resource-group-define-dependencies.md). |
| properties |Нет |Параметры конфигурации ресурса. Hello значения для свойств hello hello таким же, как hello значения, которые можно указать в тексте запроса hello hello API-интерфейса REST операции (метод PUT) toocreate hello ресурсов. Кроме того, можно указать toocreate копии массива несколько экземпляров свойства. Дополнительные сведения см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md). |
| ресурсов |Нет |Дочерние ресурсы, зависящие от определяемого ресурса hello. Предоставлять только типы ресурсов, разрешенные схемой "hello" hello родительский ресурс. Hello полное имя типа hello дочерний ресурс включает hello родительским типом ресурса, например **Microsoft.Web/sites/extensions**. Зависимость от родительского ресурса hello не предусмотрено. Ее необходимо определить явным образом. |

раздел ресурсов Hello содержит массив toodeploy ресурсы hello. Внутри каждого ресурса можно также определить набор дочерних ресурсов. Таким образом раздел ресурсов может иметь примерно следующую структуру:

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

Дополнительные сведения об определении дочерних ресурсов см. в разделе [Указание имени и типа дочернего ресурса в шаблоне Resource Manager](resource-manager-template-child-resource.md).

Hello **условие** элемент определяет, развертывается ли ресурс hello. Hello значение для этого элемента разрешает tootrue или false. Например toospecify ли развернуть новую учетную запись хранения, используйте:

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

toospecify ли развертывание виртуальных машин с помощью пароля или ключа SSH определения двух версий hello виртуальной машины в шаблон и использовать **условие** toodifferentiate использования. Передайте параметр, указывающий, какие сценарии toodeploy.

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

Пример использования пароля или SSH ключа toodeploy виртуальной машины, в разделе [имя пользователя или SSH условие шаблона](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="outputs"></a>outputs
В разделе hello выходные данные укажите значения, возвращаемые из развертывания. Например может вернуть hello URI tooaccess развернутых ресурсах.

Hello ниже приведен пример структуры hello определения выходных данных.

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| Имя элемента | Обязательно | Описание |
|:--- |:--- |:--- |
| outputName |Да |Имя hello выходное значение. Должно быть допустимым идентификатором JavaScript. |
| type |Да |Тип выходного значения hello. Выходные значения поддерживает hello же типы в качестве входных параметров шаблона. |
| value |Да |Выражение на языке шаблона, которое вычисляется и возвращается в качестве выходного значения. |

Hello пример значение, которое возвращается в разделе hello выходные данные.

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

Дополнительные сведения о работе с выходными данными см. в статье [Совместное использование состояния в шаблонах Resource Manager](best-practices-resource-manager-state.md).

## <a name="template-limits"></a>Ограничения шаблонов

Ограничить размер hello ваш шаблон too1 МБ, а также каждый параметр файловой too64 КБ. ограничение 1 МБ Hello применяется toohello конечное состояние шаблона hello после была расширена с помощью определения итеративный ресурсов и значения для переменных и параметров. 

Кроме того, ограничение распространяется на:

* 256 параметров;
* 256 переменных;
* 800 ресурсов (включая число копий);
* 64 выходных значения;
* 24 576 знаков в выражении шаблона.

Некоторые ограничения можно превысить, используя вложенные шаблоны. Дополнительные сведения см. разделе [Использование связанных шаблонов в при развертывании ресурсов Azure](resource-group-linked-templates.md). tooreduce hello число параметров, переменных или выходных данных, можно объединить несколько значений в объект. См. дополнительные сведения об [использовании объектов как параметров](resource-manager-objects-as-parameters.md).

## <a name="next-steps"></a>Дальнейшие действия
* tooview завершения шаблоны для различных типов решений, см. hello [шаблоны быстрый запуск Azure](https://azure.microsoft.com/documentation/templates/).
* Дополнительные сведения о функциях hello, можно использовать из шаблона, в разделе [функции шаблона диспетчера ресурсов Azure](resource-group-template-functions.md).
* toocombine несколько шаблонов во время развертывания, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).
* Может потребоваться toouse ресурсов, которые существуют в другой группе ресурсов. Это распространенная ситуация при работе с учетными записями хранения или виртуальными сетями, которые совместно используются в нескольких группах ресурсов. Дополнительные сведения см. в разделе hello [функции resourceId](resource-group-template-functions-resource.md#resourceid).
