---
title: "Подготовка кэша Redis с помощью Azure Resource Manager | Документация Майкрософт"
description: "Используйте шаблон диспетчера ресурсов Azure для развертывания кэша Redis для Azure."
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
ms.openlocfilehash: cce5d63e8bad2dd066cb4c28e2a8a9cb16c47953
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="b2593-103">Создание кэша Redis с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="b2593-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="b2593-104">В этом разделе вы узнаете, как создать шаблон Azure Resource Manager, который развертывает кэш Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="b2593-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="b2593-105">Кэш можно использовать с существующей учетной записи хранения для размещения данных диагностики.</span><span class="sxs-lookup"><span data-stu-id="b2593-105">The cache can be used with an existing storage account to keep diagnostic data.</span></span> <span data-ttu-id="b2593-106">Вы узнаете, как определить развертываемые ресурсы и параметры, указываемые при развертывании.</span><span class="sxs-lookup"><span data-stu-id="b2593-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="b2593-107">Этот шаблон можно использовать для собственных развертываний или настроить его в соответствии с вашими требованиями.</span><span class="sxs-lookup"><span data-stu-id="b2593-107">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="b2593-108">В настоящее время параметры диагностики являются общими для всех кэшей в одном регионе подписки.</span><span class="sxs-lookup"><span data-stu-id="b2593-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span></span> <span data-ttu-id="b2593-109">Обновление одного кэша в регионе влияет на все кэши в нем.</span><span class="sxs-lookup"><span data-stu-id="b2593-109">Updating one cache in the region affects all other caches in the region.</span></span>

<span data-ttu-id="b2593-110">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b2593-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b2593-111">Полный шаблон доступен в разделе [Шаблон кэша Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b2593-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="b2593-112">Доступны шаблоны Resource Manager для нового [уровня "Премиум"](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="b2593-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="b2593-113">Создание кэша Premium Redis с кластеризацией</span><span class="sxs-lookup"><span data-stu-id="b2593-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="b2593-114">Создание кэша Premium Redis с сохранением данных</span><span class="sxs-lookup"><span data-stu-id="b2593-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="b2593-115">Создание кэша Premium Redis с использованием VNet и дополнительной кластеризации</span><span class="sxs-lookup"><span data-stu-id="b2593-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="b2593-116">Чтобы узнать о новых шаблонах, обратитесь к статье [Шаблоны быстрого запуска Azure](https://azure.microsoft.com/documentation/templates/) и выполните поиск по критерию `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="b2593-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="b2593-117">Что именно развертывается</span><span class="sxs-lookup"><span data-stu-id="b2593-117">What you will deploy</span></span>
<span data-ttu-id="b2593-118">В этом шаблоне вы развернете кэш Azure Redis, который использует существующую учетную запись хранения для диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="b2593-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="b2593-119">Чтобы выполнить развертывание автоматически, нажмите следующую кнопку.</span><span class="sxs-lookup"><span data-stu-id="b2593-119">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="b2593-120">[![Развертывание в Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b2593-120">[![Deploy to Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="b2593-121">Параметры</span><span class="sxs-lookup"><span data-stu-id="b2593-121">Parameters</span></span>
<span data-ttu-id="b2593-122">С помощью диспетчера ресурсов Azure можно определить параметры значений, которые должны указываться на этапе развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="b2593-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="b2593-123">В шаблоне есть раздел "Параметры", содержащий все значения параметров.</span><span class="sxs-lookup"><span data-stu-id="b2593-123">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="b2593-124">Для этих значений необходимо определить параметры, которые будут зависеть от развертываемого проекта либо от среды, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="b2593-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="b2593-125">Не определяйте параметры для значений, которые не меняются.</span><span class="sxs-lookup"><span data-stu-id="b2593-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="b2593-126">Значение каждого параметра в шаблоне определяет развертываемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b2593-126">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="b2593-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="b2593-127">redisCacheLocation</span></span>
<span data-ttu-id="b2593-128">Расположение кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="b2593-128">The location of the Redis Cache.</span></span> <span data-ttu-id="b2593-129">Для наилучшей производительности используйте то же расположение, где находится приложение, которое будет пользоваться кэшем.</span><span class="sxs-lookup"><span data-stu-id="b2593-129">For best performance, use the same location as the app to be used with the cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="b2593-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="b2593-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="b2593-131">Имя существующей учетной записи хранения, которую вы хотите использовать для диагностики.</span><span class="sxs-lookup"><span data-stu-id="b2593-131">The name of the existing storage account to use for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="b2593-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="b2593-132">enableNonSslPort</span></span>
<span data-ttu-id="b2593-133">Логическое значение, указывающее, следует ли разрешить доступ к портам, отличным от SSL.</span><span class="sxs-lookup"><span data-stu-id="b2593-133">A boolean value that indicates whether to allow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="b2593-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="b2593-134">diagnosticsStatus</span></span>
<span data-ttu-id="b2593-135">Значение, указывающее, включена ли диагностика.</span><span class="sxs-lookup"><span data-stu-id="b2593-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="b2593-136">Используйте значение ON или OFF.</span><span class="sxs-lookup"><span data-stu-id="b2593-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="b2593-137">Развертываемые ресурсы</span><span class="sxs-lookup"><span data-stu-id="b2593-137">Resources to deploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="b2593-138">Кэш Redis</span><span class="sxs-lookup"><span data-stu-id="b2593-138">Redis Cache</span></span>
<span data-ttu-id="b2593-139">Создает кэш Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="b2593-139">Creates the Azure Redis Cache.</span></span>

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



## <a name="commands-to-run-deployment"></a><span data-ttu-id="b2593-140">Команды для выполнения развертывания</span><span class="sxs-lookup"><span data-stu-id="b2593-140">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="b2593-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2593-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="b2593-142">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="b2593-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


