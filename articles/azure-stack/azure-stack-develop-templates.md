---
title: "шаблоны aaaDevelop для стека Azure | Документы Microsoft"
description: "Ознакомьтесь с рекомендациями по использованию шаблона Azure Stack"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 8a5bc713-6f51-49c8-aeed-6ced0145e07b
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 01581abcb7a3616469dcd38a646734f68decd3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-considerations"></a>Рекомендации по использованию шаблона Azure Resource Manager
При разработке приложения, он является переносимость шаблона важные tooensure между Azure и Azure стека.  Этот раздел содержит рекомендации по разработке диспетчера ресурсов Azure [шаблоны](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), поэтому можно прототип приложения и тестов развертывания в Azure без среды стека Azure tooan доступа.

## <a name="public-namespaces"></a>Общедоступные пространства имен
Поскольку стек Azure размещается в центре обработки данных, она имеет другую службу пространств имен конечных точек, чем hello общедоступное облако Azure. В результате жестко закодировано общедоступные конечные точки в шаблоны диспетчера ресурсов ошибкой при попытке toodeploy их tooAzure стека. Вместо этого можно использовать hello *ссылки* и *объединение* toodynamically функция сборки hello конечной точки службы в зависимости от значения, полученные от поставщика ресурсов hello во время развертывания. Например, вместо того чтобы задавать *blob.core.windows.net* в шаблоне, получить hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically задать hello *osDisk.URI* Конечная точка:

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a>Управление версиями API
В Azure и Azure Stack могут быть разные версии служб Azure. Каждый ресурс требует hello apiVersion атрибут, определяющий возможности hello. совместимость версий tooensure API в Azure стек, выполнив hello приведены допустимые версии API для каждого поставщика ресурсов.

| Поставщик ресурсов | версия_API |
| --- | --- |
| Среда выполнения приложений |`'2015-06-15'` |
| Сеть |`'2015-06-15'`, `'2015-05-01-preview'` |
| Хранилище |`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'` |
| Хранилище ключей | `'2015-06-01'` |
| Служба приложений |`'2015-08-01'` |
| MySQL |`'2015-09-01'` |
| SQL |`'2014-04-01-preview'` |

## <a name="template-functions"></a>Функции шаблонов
Диспетчер ресурсов [функции](../azure-resource-manager/resource-group-template-functions.md) предоставляют необходимые toobuild возможности динамических шаблонов. Например, можно использовать функции для выполнения следующих задач.

* Объединение или обрезание строк. 
* Создание ссылок на значения других ресурсов.
* Итерации по toodeploy ресурсы нескольких экземпляров 

При создании шаблонов, некоторые функции недоступны в пакете средств разработки Azure стека и не должны использоваться. Это следующие функции:

* Skip
* Take

## <a name="resource-location"></a>Расположение ресурса
Шаблоны диспетчера ресурсов использовать расположение атрибута tooplace ресурсы во время развертывания. В Azure расположения ссылаться области tooa как Запад США или Южной Америке. В Azure Stack используются другие расположения, так как Azure Stack находится в вашем центре обработки данных.  шаблоны tooensure переносимые между Azure и Azure стека, должно указывать расположение группы ресурсов hello при развертывании отдельных ресурсов. Это можно сделать с помощью `[resourceGroup().Location]` tooensure наследуют все ресурсы hello расположение группы ресурсов.  Hello следующий фрагмент шаблона диспетчера ресурсов приведен пример использования этой функции при развертывании учетной записи хранилища.

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used toostore hello VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]


## <a name="next-steps"></a>Дальнейшие действия
* [Развертывание шаблонов с помощью PowerShell](azure-stack-deploy-template-powershell.md)
* [Развертывание шаблонов с помощью интерфейса командной строки Azure](azure-stack-deploy-template-command-line.md)
* [Развертывание шаблонов с помощью Visual Studio](azure-stack-deploy-template-visual-studio.md)

