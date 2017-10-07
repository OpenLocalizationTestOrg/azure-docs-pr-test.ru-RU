---
title: "aaaProvision кэша Redis с использованием диспетчера ресурсов Azure | Документы Microsoft"
description: "С помощью шаблона Azure Resource Manager toodeploy кэш Azure Redis."
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a>Создание кэша Redis с помощью шаблона
В этом разделе вы узнаете, как toocreate шаблона диспетчера ресурсов Azure, которая выполняет развертывание кэша Redis Azure. Hello кэша может использоваться с существующие данные учетной записи хранилища tookeep диагностики. Вы также узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello. Этот шаблон используется для собственных развертывания или настройте его toomeet вашим требованиям.

В настоящее время, диагностические параметры которого являются общими для всех кэшей в hello же регионе для подписки. Обновление один кэш в регионе hello оказывает влияние на другие кэши в регионе hello.

Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Полный шаблон hello, см. [кэша Redis шаблона](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).

> [!NOTE]
> Шаблоны диспетчера ресурсов для нового hello [уровня Premium](cache-premium-tier-intro.md) доступны. 
> 
> * [Создание кэша Premium Redis с кластеризацией](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [Создание кэша Premium Redis с сохранением данных](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [Создание кэша Premium Redis с использованием VNet и дополнительной кластеризации](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> toocheck для hello последние шаблоны, в разделе [шаблоны быстрый запуск Azure](https://azure.microsoft.com/documentation/templates/) и выполните поиск `Redis Cache`.
> 
> 

## <a name="what-you-will-deploy"></a>Что именно развертывается
В этом шаблоне вы развернете кэш Azure Redis, который использует существующую учетную запись хранения для диагностических данных.

toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:

[![Развертывание tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)

## <a name="parameters"></a>Параметры
С помощью диспетчера ресурсов Azure можно определить параметры для значения требуется toospecify при развертывании шаблона hello. шаблон Hello имеется раздел с именем параметров, содержащий все значения параметров hello.
Следует определить параметр для тех значений, которые отличаются на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание. Определяет параметры для hello значения, которые всегда остаются одинаковыми. Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются. 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a>redisCacheLocation
расположение Hello hello кэша Redis. Для достижения оптимальной производительности используйте hello же, как используется с кэшем hello toobe приложения hello.

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a>existingDiagnosticsStorageAccountName
Hello имя hello существующего хранилища учетной записи toouse для диагностики. 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a>enableNonSslPort
Логическое значение, указывающее, доступен ли tooallow через порты не SSL.

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a>diagnosticsStatus
Значение, указывающее, включена ли диагностика. Используйте значение ON или OFF.

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a>Toodeploy ресурсы
### <a name="redis-cache"></a>Кэш Redis
Создает hello кэша Redis для Azure.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-toorun-deployment"></a>Команды toorun развертывания
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a>Инфраструктура CLI Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


