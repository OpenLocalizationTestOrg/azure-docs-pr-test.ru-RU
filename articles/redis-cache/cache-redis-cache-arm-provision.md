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
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="1fa96-103">Создание кэша Redis с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="1fa96-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="1fa96-104">В этом разделе вы узнаете, как toocreate шаблона диспетчера ресурсов Azure, которая выполняет развертывание кэша Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="1fa96-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="1fa96-105">Hello кэша может использоваться с существующие данные учетной записи хранилища tookeep диагностики.</span><span class="sxs-lookup"><span data-stu-id="1fa96-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="1fa96-106">Вы также узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="1fa96-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="1fa96-107">Этот шаблон используется для собственных развертывания или настройте его toomeet вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="1fa96-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="1fa96-108">В настоящее время, диагностические параметры которого являются общими для всех кэшей в hello же регионе для подписки.</span><span class="sxs-lookup"><span data-stu-id="1fa96-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="1fa96-109">Обновление один кэш в регионе hello оказывает влияние на другие кэши в регионе hello.</span><span class="sxs-lookup"><span data-stu-id="1fa96-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="1fa96-110">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1fa96-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="1fa96-111">Полный шаблон hello, см. [кэша Redis шаблона](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="1fa96-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="1fa96-112">Шаблоны диспетчера ресурсов для нового hello [уровня Premium](cache-premium-tier-intro.md) доступны.</span><span class="sxs-lookup"><span data-stu-id="1fa96-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="1fa96-113">Создание кэша Premium Redis с кластеризацией</span><span class="sxs-lookup"><span data-stu-id="1fa96-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="1fa96-114">Создание кэша Premium Redis с сохранением данных</span><span class="sxs-lookup"><span data-stu-id="1fa96-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="1fa96-115">Создание кэша Premium Redis с использованием VNet и дополнительной кластеризации</span><span class="sxs-lookup"><span data-stu-id="1fa96-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="1fa96-116">toocheck для hello последние шаблоны, в разделе [шаблоны быстрый запуск Azure](https://azure.microsoft.com/documentation/templates/) и выполните поиск `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="1fa96-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="1fa96-117">Что именно развертывается</span><span class="sxs-lookup"><span data-stu-id="1fa96-117">What you will deploy</span></span>
<span data-ttu-id="1fa96-118">В этом шаблоне вы развернете кэш Azure Redis, который использует существующую учетную запись хранения для диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="1fa96-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="1fa96-119">toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="1fa96-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="1fa96-120">[![Развертывание tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="1fa96-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="1fa96-121">Параметры</span><span class="sxs-lookup"><span data-stu-id="1fa96-121">Parameters</span></span>
<span data-ttu-id="1fa96-122">С помощью диспетчера ресурсов Azure можно определить параметры для значения требуется toospecify при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="1fa96-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="1fa96-123">шаблон Hello имеется раздел с именем параметров, содержащий все значения параметров hello.</span><span class="sxs-lookup"><span data-stu-id="1fa96-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="1fa96-124">Следует определить параметр для тех значений, которые отличаются на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="1fa96-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="1fa96-125">Определяет параметры для hello значения, которые всегда остаются одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="1fa96-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="1fa96-126">Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="1fa96-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="1fa96-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="1fa96-127">redisCacheLocation</span></span>
<span data-ttu-id="1fa96-128">расположение Hello hello кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="1fa96-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="1fa96-129">Для достижения оптимальной производительности используйте hello же, как используется с кэшем hello toobe приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1fa96-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="1fa96-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="1fa96-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="1fa96-131">Hello имя hello существующего хранилища учетной записи toouse для диагностики.</span><span class="sxs-lookup"><span data-stu-id="1fa96-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="1fa96-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="1fa96-132">enableNonSslPort</span></span>
<span data-ttu-id="1fa96-133">Логическое значение, указывающее, доступен ли tooallow через порты не SSL.</span><span class="sxs-lookup"><span data-stu-id="1fa96-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="1fa96-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="1fa96-134">diagnosticsStatus</span></span>
<span data-ttu-id="1fa96-135">Значение, указывающее, включена ли диагностика.</span><span class="sxs-lookup"><span data-stu-id="1fa96-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="1fa96-136">Используйте значение ON или OFF.</span><span class="sxs-lookup"><span data-stu-id="1fa96-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="1fa96-137">Toodeploy ресурсы</span><span class="sxs-lookup"><span data-stu-id="1fa96-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="1fa96-138">Кэш Redis</span><span class="sxs-lookup"><span data-stu-id="1fa96-138">Redis Cache</span></span>
<span data-ttu-id="1fa96-139">Создает hello кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="1fa96-139">Creates hello Azure Redis Cache.</span></span>

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



## <a name="commands-toorun-deployment"></a><span data-ttu-id="1fa96-140">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="1fa96-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="1fa96-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fa96-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="1fa96-142">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="1fa96-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


