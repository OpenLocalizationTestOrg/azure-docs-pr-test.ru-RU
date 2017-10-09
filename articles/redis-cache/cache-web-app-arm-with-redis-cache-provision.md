---
title: "aaaProvision веб-приложения в кэш Redis"
description: "Использование диспетчера ресурсов Azure шаблона toodeploy веб-приложения с кэшем Redis."
services: app-service
documentationcenter: 
author: steved0x
manager: erickson-doug
editor: 
ms.assetid: 6e99c71f-ef8e-4570-a307-e4c059e60c35
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: b95b5e230dc40c1157940c2017cba836975b6930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="67725-103">Создание веб-приложения и кэша Redis с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="67725-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="67725-104">В этом разделе вы узнаете, как toocreate шаблона Azure Resource Manager, которая развертывает веб-приложение Azure с помощью кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="67725-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="67725-105">Вы узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="67725-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="67725-106">Этот шаблон используется для собственных развертывания или настройте его toomeet вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="67725-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="67725-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67725-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="67725-108">Полный шаблон hello, см. [веб-приложения с помощью шаблона кэша Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="67725-108">For hello complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="67725-109">Что именно развертывается</span><span class="sxs-lookup"><span data-stu-id="67725-109">What you will deploy</span></span>
<span data-ttu-id="67725-110">В этом шаблоне будут развернуты перечисленные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="67725-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="67725-111">Веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="67725-111">Azure Web App</span></span>
* <span data-ttu-id="67725-112">Кэш Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="67725-112">Azure Redis Cache.</span></span>

<span data-ttu-id="67725-113">toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="67725-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="67725-114">[![Развертывание tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="67725-114">[![Deploy tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="67725-115">Параметры toospecify</span><span class="sxs-lookup"><span data-stu-id="67725-115">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="67725-116">Переменные для имен</span><span class="sxs-lookup"><span data-stu-id="67725-116">Variables for names</span></span>
<span data-ttu-id="67725-117">Этот шаблон использует имена переменных tooconstruct hello ресурсы.</span><span class="sxs-lookup"><span data-stu-id="67725-117">This template uses variables tooconstruct names for hello resources.</span></span> <span data-ttu-id="67725-118">Она использует hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) функции tooconstruct значение в соответствии с идентификатор группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67725-118">It uses hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function tooconstruct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="67725-119">Toodeploy ресурсы</span><span class="sxs-lookup"><span data-stu-id="67725-119">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="67725-120">Кэш Redis</span><span class="sxs-lookup"><span data-stu-id="67725-120">Redis Cache</span></span>
<span data-ttu-id="67725-121">Создает hello кэша Redis для Azure, используемое с веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="67725-121">Creates hello Azure Redis Cache that is used with hello web app.</span></span> <span data-ttu-id="67725-122">указано имя Hello hello кэша в hello **cacheName** переменной.</span><span class="sxs-lookup"><span data-stu-id="67725-122">hello name of hello cache is specified in hello **cacheName** variable.</span></span>

<span data-ttu-id="67725-123">шаблон Hello создает кэш hello hello местоположения hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67725-123">hello template creates hello cache in hello same location as hello resource group.</span></span>

    {
      "name": "[variables('cacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [ ],
      "tags": {
        "displayName": "cache"
      },
      "properties": {
        "sku": {
          "name": "[parameters('cacheSKUName')]",
          "family": "[parameters('cacheSKUFamily')]",
          "capacity": "[parameters('cacheSKUCapacity')]"
        }
      }
    }


### <a name="web-app"></a><span data-ttu-id="67725-124">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="67725-124">Web app</span></span>
<span data-ttu-id="67725-125">Создает hello веб-приложения с именем, указанным в hello **webSiteName** переменной.</span><span class="sxs-lookup"><span data-stu-id="67725-125">Creates hello web app with name specified in hello **webSiteName** variable.</span></span>

<span data-ttu-id="67725-126">Обратите внимание, что веб-приложения hello настроен с приложением, свойства, позволяющие ему toowork с hello кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="67725-126">Notice that hello web app is configured with app setting properties that enable it toowork with hello Redis Cache.</span></span> <span data-ttu-id="67725-127">Эти параметры приложения динамически создаются на основании значений, предоставленных во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="67725-127">This app settings are dynamically created based on values provided during deployment.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Web/serverFarms/', variables('hostingPlanName'))]",
        "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "appsettings",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', variables('webSiteName'))]",
            "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
          ],
          "properties": {
            "CacheConnection": "[concat(variables('cacheName'),'.redis.cache.windows.net,abortConnect=false,ssl=true,password=', listKeys(resourceId('Microsoft.Cache/Redis', variables('cacheName')), '2015-08-01').primaryKey)]"
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="67725-128">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="67725-128">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="67725-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="67725-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="67725-130">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="67725-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
