---
title: "группы ресурсов toomultiple aaaDeploy ресурсы Azure | Документы Microsoft"
description: "Показывает, как группировать tootarget больше, чем один ресурс Azure во время развертывания."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a>Развертывание toomore ресурсы Azure, чем одной группы ресурсов

Как правило все ресурсы hello развернуть в ваш шаблон tooa единой группы ресурсов. Однако существуют сценарии, где требуется набор ресурсов toodeploy друг с другом, но поместить их в разные группы ресурсов. Например может потребоваться toodeploy hello резервного копирования виртуальной машины для Azure Site Recovery tooa отдельной группе ресурсов и расположение. Диспетчер ресурсов позволяет toouse вложенные шаблоны tootarget разные группы ресурсов чем hello группы ресурсов, используемой для hello родительского шаблона.

Группа ресурсов Hello находится hello жизненный цикл контейнера для приложения hello и его ресурсы. Создать группу ресурсов hello за пределами шаблона hello и укажите tootarget группы ресурсов hello во время развертывания. Введение tooresource группы, в разделе [Обзор диспетчера ресурсов Azure](resource-group-overview.md).

## <a name="example-template"></a>Пример шаблона

tootarget другой ресурс, необходимо использовать шаблон вложенной или связанной во время развертывания. Hello `Microsoft.Resources/deployments` обеспечивает `resourceGroup` параметр, который позволяет toospecify другой группе ресурсов для hello вложенные развертывания. Все группы ресурсов hello должен существовать до запуска развертывания hello. Hello примере развертывает две учетные записи хранилища — один в группе ресурсов hello, указанное во время развертывания и по одному в группу ресурсов с именем `crossResourceGroupDeployment`:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

Если задать `resourceGroup` toohello имя группы ресурсов, который не существует, развертывание hello завершается с ошибкой. Если не указано значение для `resourceGroup`, диспетчер ресурсов использует hello родительской группы ресурсов.  

## <a name="deploy-hello-template"></a>Развертывание шаблона hello

Пример шаблона toodeploy hello, можно использовать портал hello, Azure PowerShell или Azure CLI. Используйте выпуски этих средств начиная с мая 2017 года. Hello примерах предполагается, сохраненные локально hello шаблон в файл с именем **crossrgdeployment.json**.

При использовании PowerShell выполните следующее:

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

При использовании Azure CLI выполните следующее:

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

После завершения развертывания вы увидите две группы ресурсов, в каждой из которых содержится учетная запись хранения.

## <a name="use-resourcegroup-function"></a>Использование функции resourceGroup()

Для кросс-развертывания группы ресурсов, hello [resouceGroup() функция](resource-group-template-functions-resource.md#resourcegroup) разрешает различаются в зависимости от способа задания hello вложенных шаблонов. 

При внедрении один шаблон в другой шаблон resouceGroup() в вложенных шаблонов hello устраняет toohello родительской группы ресурсов. Внедренные шаблон использует hello следующий формат:

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

При связывании отдельный шаблон tooa resouceGroup() в hello связанного шаблона разрешает toohello группы вложенных ресурсов. Связанный шаблон использует hello следующий формат:

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия

* toodefine параметры в шаблоне, в статье toounderstand [понять структуру hello и синтаксис шаблоны Azure Resource Manager](resource-group-authoring-templates.md).
* Советы по устранению распространенных ошибок развертывания см. в разделе [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Сведения о развертывании шаблона, которому нужен токен SAS, см. в статье [Развертывание частного шаблона с помощью маркера SAS](resource-manager-powershell-sas-token.md).
