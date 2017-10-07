---
title: "aaaExport шаблона диспетчера ресурсов с помощью Azure PowerShell | Документы Microsoft"
description: "С помощью диспетчера ресурсов Azure и Azure PowerShell tooexport шаблона из группы ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 9a239b7bce8209326c0e267a4d3d69f7014bdaed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a>Экспорт шаблонов Azure Resource Manager с помощью PowerShell

Диспетчер ресурсов позволяет tooexport шаблона диспетчера ресурсов от существующих ресурсов в вашей подписке. Можно использовать, созданного шаблона toolearn о hello шаблона синтаксис или tooautomate hello повторное развертывание решения при необходимости.

Это важные toonote, что существует два разных способа tooexport шаблона:

* Вы можете экспортировать hello фактическое шаблона, который использовался для развертывания. экспортированный шаблон Hello включает все параметры hello и переменные, точно так, как они выглядели в исходном шаблоне hello. Этот подход полезен при необходимости tooretrieve шаблона.
* Вы можете экспортировать шаблон, который представляет текущее состояние группы ресурсов hello hello. экспортированный шаблон Hello не основывается на любой шаблон, который использовался для развертывания. Вместо этого он создает шаблон, который является моментальным снимком, группа ресурсов «hello». экспортированный шаблон Hello имеет много жестко запрограммированных значений и, возможно, не все параметры, как обычно при определении. Этот подход полезен, если вы изменили hello группы ресурсов. Теперь требуется группа ресурсов hello toocapture как шаблон.

В этой статье показаны оба способа.

## <a name="deploy-a-solution"></a>Развертывание решения

Оба tooillustrate подходы для экспорта шаблона, давайте начнем, развернув решение tooyour подписки. Если уже есть группа ресурсов в подписке, что требуется tooexport, у вас toodeploy этого решения. Однако hello оставшейся части этой статьи относится toohello шаблона для этого решения. Пример сценария Hello развертывает учетной записи хранилища.

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a>Сохранение шаблона из журнала развертываний

Можно извлечь шаблон из журнала развертывания с помощью hello [AzureRmResourceGroupDeploymentTemplate Сохранить](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) команды. Следующий пример сохраняет hello шаблона ранее развертывание Hello:

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

Он возвращает местоположение hello hello шаблона.

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

Откройте файл hello и обратите внимание, что hello точное шаблон, который используется для развертывания. Hello параметры и переменные соответствуют шаблону hello из GitHub. Этот шаблон можно развернуть повторно.

## <a name="export-resource-group-as-template"></a>Экспорт группы ресурсов в виде шаблона

Вместо извлечения шаблона из журнала развертывания hello, вы можете получить шаблон, который представляет текущее состояние hello группы ресурсов с помощью hello [AzureRmResourceGroup экспорта](/powershell/module/azurerm.resources/export-azurermresourcegroup) команды. Эта команда используется в том случае, если вы внесли многие группы ресурсов tooyour изменения и не существующий шаблон представляет все изменения hello.

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

Он возвращает местоположение hello hello шаблона.

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

Откройте файл hello и обратите внимание, что это отличается от шаблона hello в GitHub. У него другие параметры и нет переменных. хранилище Hello SKU и расположение являются жестко toovalues. Hello пример hello экспортированный шаблон, но ваш шаблон имеет имя параметра немного отличается.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Можно повторно развернуть этот шаблон, но он требует угадывания уникальное имя для учетной записи хранения hello. Имя параметра Hello немного отличается.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a>Настройка экспортированного шаблона

Вы можете изменить этот шаблон toomake его toouse проще и гибче. tooallow для дополнительных местоположений, изменение hello расположение свойство toouse hello местоположения hello группа ресурсов:

```json
"location": "[resourceGroup().location]",
```

tooavoid наличие tooguess uniques имени для учетной записи хранилища, удаление параметра hello hello имени учетной записи хранения. Добавьте параметр для суффикса имени хранилища и номер SKU хранилища:

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

Добавьте переменную, которая создает hello имя учетной записи хранилища с помощью функции hello uniqueString:

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

Задайте имя hello переменной toohello учетной записи хранилища hello:

```json
"name": "[variables('storageAccountName')]",
```

Задайте для параметра toohello hello SKU:

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

Ваш шаблон теперь выглядит так:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Повторное развертывание hello измененный шаблон.

## <a name="next-steps"></a>Дальнейшие действия
* Сведения об использовании портала tooexport hello шаблона см. в разделе [Экспорт шаблона диспетчера ресурсов Azure с существующие ресурсы](resource-manager-export-template.md).
* toodefine параметры в шаблоне, в разделе [разработки шаблонов](resource-group-authoring-templates.md#parameters).
* Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).
