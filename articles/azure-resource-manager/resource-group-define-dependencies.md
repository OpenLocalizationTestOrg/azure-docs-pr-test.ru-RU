---
title: "порядок развертывания aaaSet для ресурсов Azure | Документы Microsoft"
description: "Описание способа развертывания tooset один ресурс как зависимость от другого ресурса во время развертывания tooensure ресурсы в правильном порядке hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a>Задать порядок hello развертывания ресурсов в шаблоны Azure Resource Manager
Для данного ресурса может быть другие ресурсы, которые должны существовать до развертывания ресурсов hello. Например SQL server должен существовать прежде чем toodeploy базы данных SQL. Вы определять эту связь, помечая один ресурс как зависимость от hello другого ресурса. Определение зависимостей с hello **dependsOn** элемент, или с помощью hello **ссылки** функции. 

Диспетчер ресурсов оценивает hello зависимости между ресурсами и развертывает их в порядке зависимости. Если ресурсы не зависят друг от друга, диспетчер ресурсов развертывает их параллельно. Требуется toodefine зависимости только для ресурсов, развернутых в hello того же шаблона. 

## <a name="dependson"></a>Свойство dependsOn
В шаблоне элемент dependsOn hello позволяет toodefine один ресурс в зависимости от одного или нескольких ресурсов. В качестве значения свойства может выступать список имен ресурсов с разделителями-запятыми. 

Hello пример набора масштабирования виртуальных машин, который зависит от подсистемы балансировки нагрузки, виртуальной сети и цикл, который создает несколько учетных записей хранения. Эти другие ресурсы в следующий пример hello не отображаются, но им нужны tooexist в другом месте в шаблоне hello.

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

В предыдущих пример hello, зависимость включается hello ресурсов, которые создаются с помощью цикла копирования с именем **storageLoop**. Пример см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).

При определении зависимостей, можно включить hello ресурсов поставщика пространства имен и ресурса типа tooavoid неоднозначности. Например tooclarify, балансировки нагрузки и виртуальной сети, которая может иметь hello такими же именами, как другие ресурсы hello используйте следующий формат:

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

Хотя может быть держите toouse dependsOn toomap связи между ресурсов, это важные toounderstand, почему вы пишете код. Например, toodocument как ресурсы связаны между собой, dependsOn не hello правильного подхода. Не удается запросить, какие ресурсы были определены в элементе dependsOn hello после развертывания. Использование свойства dependsOn потенциально влияет на время развертывания, так как Resource Manager не может выполнять развертывание двух зависимых ресурсов параллельно. toodocument связи между ресурсами, вместо этого использовать [привязке ресурсов](/rest/api/resources/resourcelinks).

## <a name="child-resources"></a>Дочерние ресурсы
Свойства ресурсов Hello можно toospecify дочерние ресурсы, определяемый toohello связанный ресурс. Дочерние ресурсы можно определять максимум на пяти нижестоящих уровнях. Очень важно toonote, неявное зависимостей не созданы между дочерней и родительской ресурса hello. Если требуется hello дочерних ресурсов toobe после hello родительский ресурс развертывание, необходимо явно указать зависимость со свойством dependsOn hello. 

Каждый родительский ресурс принимает в качестве дочерних ресурсов только определенные типы ресурсов. Hello приняты указанные типы ресурсов в hello [схема шаблона](https://github.com/Azure/azure-resource-manager-schemas) hello родительского ресурса. Hello имя типа ресурса дочерних содержит hello типа hello родительского ресурса, например **Microsoft.Web/sites/config** и **Microsoft.Web/sites/extensions** являются оба дочерними ресурсами hello  **Microsoft.Web/sites**.

Следующий пример Hello показывает SQL server и базы данных SQL. Обратите внимание, что явных зависимостей определена между hello базы данных SQL и SQL server, несмотря на то, что hello базы данных является дочерним элементом сервера hello.

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a>Функция reference
Hello [ссылки на функцию](resource-group-template-functions-resource.md#reference) включает выражение tooderive свое значение из других пар имен и значений JSON или ресурсов среды выполнения. Выражения со ссылками неявно объявляют, что один ресурс зависит от другого. Hello общие выглядит следующим образом:

```json
reference('resourceName').propertyPath
```

В следующем примере hello конечной точкой CDN явно зависит от профиля CDN hello и неявно зависит от веб-приложения.

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

Можно использовать этот элемент или hello зависимости toospecify элемент dependsOn, но не требуется для hello toouse оба же зависимый ресурс. По возможности используйте tooavoid неявные ссылки, добавление ненужные зависимости.

toolearn более, в разделе [ссылки на функцию](resource-group-template-functions-resource.md#reference).

## <a name="recommendations-for-setting-dependencies"></a>Рекомендации по установке зависимостей

При определении того, какие зависимости tooset, используйте hello, следование правилам:

* Устанавливайте как можно меньше зависимостей.
* Назначайте дочерний ресурс зависимым от его родительского ресурса.
* Используйте hello **ссылки** функции tooset неявные зависимости между ресурсами, которые должны tooshare свойство. Не добавляйте явную зависимость (**dependsOn**), если уже определена неявная зависимость. Этот подход уменьшает риск hello ненужные зависимости. 
* Задавайте зависимость, когда ресурс не может быть **создан** без функциональных возможностей другого ресурса. Не задавайте зависимости ресурсов hello взаимодействовать только после развертывания.
* Позвольте зависимостям задействоваться последовательно, не задавая их явно. Например виртуальной машины зависит от виртуального сетевого интерфейса и hello виртуального сетевого интерфейса зависит от виртуальной сети и общедоступные IP-адреса. Таким образом развернутые ресурсы после того как все три — hello виртуальной машины, но не задано явно hello виртуальной машины как зависимость от всех трех ресурсов. Этот подход поясняется порядок зависимостей hello и делает его проще шаблон toochange hello позже.
* Если значение может быть определено до развертывания, попробуйте выполните развертывание ресурсов hello без зависимостей. Например если значение конфигурации должен hello имя другого ресурса, может не требоваться зависимость. В этом руководстве не всегда работает, поскольку некоторые ресурсы проверять существование hello hello другого ресурса. Если произошла ошибка, добавьте зависимость. 

Resource Manager выявляет циклические зависимости во время проверки шаблона. Если появится сообщение о том, что существует циклическая зависимость, оценка toosee ваш шаблон, если все зависимости не нужны и может быть удален. Если удаление зависимостей не работает, можно избежать, переместив некоторые операции развертывания в дочерние ресурсы, которые развертываются после hello ресурсов, имеющих циклическую зависимость hello циклические зависимости. Предположим, например, две виртуальные машины развертываются, но необходимо задать свойства для каждого из них, которые ссылаются другие toohello. Их можно развернуть в hello следующий порядок:

1. vm1.
2. vm2.
3. Расширение на vm1 зависит от vm1 и vm2. расширение Hello задает значения по vm1, получаемый от vm2.
4. Расширение на vm2 зависит от vm1 и vm2. расширение Hello задает значения по vm2, получаемый от vm1.

Сведения об оценке hello порядок развертывания и устранять ошибки зависимостей в разделе [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md).

## <a name="next-steps"></a>Дальнейшие действия
* toolearn об устранении неполадок зависимости во время развертывания, в разделе [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md).
* toolearn о создании шаблонов диспетчера ресурсов Azure в разделе [разработки шаблонов](resource-group-authoring-templates.md). 
* Список доступных функций hello в шаблоне см. в разделе [функции шаблона](resource-group-template-functions.md).

