---
title: "aaaCreate логику приложения, с помощью шаблона в Azure | Документы Microsoft"
description: "Используйте toodeploy шаблона диспетчера ресурсов Azure приложение логики для определения рабочих процессов."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a>Создание приложения логики с помощью шаблона
Шаблоны предоставляют toouse быстро разные соединители внутри приложения логики. Логику приложений включает шаблоны Azure Resource Manager для toocreate приложения логики, который можно использовать toodefine бизнес-процессов. Можно определить, какие ресурсы развернуты и как параметры toodefine при развертывании приложения логики. Можно использовать этот шаблон для собственных бизнес-сценариев, или настроить его toomeet вашим требованиям.

Дополнительные сведения о свойствах приложения hello логику в разделе [логику приложения рабочего процесса управления API](https://msdn.microsoft.com/library/azure/mt643788.aspx). 

Примеры само определение hello см. в разделе [Автор приложения логики определения](logic-apps-author-definitions.md). 

Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Полный шаблон hello, см. [шаблон приложения логики](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).

## <a name="what-you-deploy"></a>Что будет развернуто?
С помощью этого шаблона развертывается приложение логики.

Развертывание hello toorun автоматически, выберите hello следующие кнопки:  

[![Развертывание tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

## <a name="parameters"></a>Параметры
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a>testUri
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a>Toodeploy ресурсы
### <a name="logic-app"></a>Приложение логики
Создание приложения hello логики.

шаблоны Hello использует значение параметра для имени приложения hello логику. Задает расположение hello hello логику приложения toohello же расположении, что группа ресурсов hello. 

Это конкретное определение выполняется один раз в час, а команды ping hello в расположении, указанном в hello **testUri** параметра. 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-toorun-deployment"></a>Команды toorun развертывания
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Инфраструктура CLI Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



