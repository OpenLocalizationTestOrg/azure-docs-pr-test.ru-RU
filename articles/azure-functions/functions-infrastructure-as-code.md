---
title: "aaaAutomate ресурсов развертывания для приложения функции в функции Azure | Документы Microsoft"
description: "Узнайте, как toobuild шаблона Azure Resource Manager, которая развертывает приложение функции."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "функции Azure, функции, независимая от сервера архитектура, инфраструктура как код, Azure Resource Manager"
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="49a54-104">Автоматизация развертывания ресурсов приложения-функции для службы "Функции Azure"</span><span class="sxs-lookup"><span data-stu-id="49a54-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="49a54-105">Можно использовать toodeploy шаблона диспетчера ресурсов Azure приложения функции.</span><span class="sxs-lookup"><span data-stu-id="49a54-105">You can use an Azure Resource Manager template toodeploy a function app.</span></span> <span data-ttu-id="49a54-106">В этой статье рассматриваются hello необходимые ресурсы и параметры для этого.</span><span class="sxs-lookup"><span data-stu-id="49a54-106">This article outlines hello required resources and parameters for doing so.</span></span> <span data-ttu-id="49a54-107">Могут потребоваться дополнительные ресурсы toodeploy, в зависимости от hello [триггеры и привязки](functions-triggers-bindings.md) в приложении функции.</span><span class="sxs-lookup"><span data-stu-id="49a54-107">You might need toodeploy additional resources, depending on hello [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="49a54-108">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="49a54-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="49a54-109">Примеры шаблонов см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="49a54-109">For sample templates, see:</span></span>
- <span data-ttu-id="49a54-110">[Function app on Consumption plan] (Приложение-функция в плане потребления);</span><span class="sxs-lookup"><span data-stu-id="49a54-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="49a54-111">[Function app on Azure App Service plan] (Приложение-функция в плане службы приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="49a54-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="49a54-112">Необходимые ресурсы</span><span class="sxs-lookup"><span data-stu-id="49a54-112">Required resources</span></span>

<span data-ttu-id="49a54-113">Для приложения-функции требуются следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="49a54-113">A function app requires these resources:</span></span>

* <span data-ttu-id="49a54-114">[Учетная запись хранения Azure.](../storage/index.md)</span><span class="sxs-lookup"><span data-stu-id="49a54-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="49a54-115">План размещения (план потребления или план службы приложений).</span><span class="sxs-lookup"><span data-stu-id="49a54-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="49a54-116">Приложение-функция.</span><span class="sxs-lookup"><span data-stu-id="49a54-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="49a54-117">Учетная запись хранения</span><span class="sxs-lookup"><span data-stu-id="49a54-117">Storage account</span></span>

<span data-ttu-id="49a54-118">Учетная запись хранения Azure — обязательный ресурс для приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="49a54-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="49a54-119">Необходима учетная запись общего назначения, поддерживающая большие двоичные объекты, таблицы, очереди и файлы.</span><span class="sxs-lookup"><span data-stu-id="49a54-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="49a54-120">Дополнительные сведения см. в разделе [Требования к учетной записи хранения](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="49a54-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

<span data-ttu-id="49a54-121">Кроме того, hello свойства `AzureWebJobsStorage` и `AzureWebJobsDashboard` должен быть указан как параметры приложения в конфигурации сайта hello.</span><span class="sxs-lookup"><span data-stu-id="49a54-121">In addition, hello properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in hello site configuration.</span></span> <span data-ttu-id="49a54-122">Среда выполнения Azure функции Hello использует hello `AzureWebJobsStorage` внутренние очереди toocreate строка соединения.</span><span class="sxs-lookup"><span data-stu-id="49a54-122">hello Azure Functions runtime uses hello `AzureWebJobsStorage` connection string toocreate internal queues.</span></span> <span data-ttu-id="49a54-123">Здравствуйте, строка подключения `AzureWebJobsDashboard` — используется toolog tooAzure таблиц хранения и управления питанием hello **монитор** вкладка на портале hello.</span><span class="sxs-lookup"><span data-stu-id="49a54-123">hello connection string `AzureWebJobsDashboard` is used toolog tooAzure Table storage and power hello **Monitor** tab in hello portal.</span></span>

<span data-ttu-id="49a54-124">Эти свойства задаются в hello `appSettings` коллекции в hello `siteConfig` объекта:</span><span class="sxs-lookup"><span data-stu-id="49a54-124">These properties are specified in hello `appSettings` collection in hello `siteConfig` object:</span></span>

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a><span data-ttu-id="49a54-125">План размещения</span><span class="sxs-lookup"><span data-stu-id="49a54-125">Hosting plan</span></span>

<span data-ttu-id="49a54-126">Определение Hello hello план размещения зависит от, используется ли план потребления или службы приложений.</span><span class="sxs-lookup"><span data-stu-id="49a54-126">hello definition of hello hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="49a54-127">В разделе [развертывание приложения функции hello потребления плана](#consumption) и [развертывание приложения функции на hello план служб приложений](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="49a54-127">See [Deploy a function app on hello Consumption plan](#consumption) and [Deploy a function app on hello App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="49a54-128">Приложение-функция</span><span class="sxs-lookup"><span data-stu-id="49a54-128">Function app</span></span>

<span data-ttu-id="49a54-129">ресурс приложения Hello функций определяется с помощью ресурса типа **Microsoft.Web/Site** и вид **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="49a54-129">hello function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a><span data-ttu-id="49a54-130">Развертывание приложения в плане использования hello функции</span><span class="sxs-lookup"><span data-stu-id="49a54-130">Deploy a function app on hello Consumption plan</span></span>

<span data-ttu-id="49a54-131">Вы можете запустить приложение функции в двух разных режимах: hello потребления план и hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="49a54-131">You can run a function app in two different modes: hello Consumption plan and hello App Service plan.</span></span> <span data-ttu-id="49a54-132">план потребления Hello автоматически размещает вычислительной мощности, когда кода выполняется, при необходимости toohandle загрузки масштабируемостью и затем масштабируется, если код не выполняется.</span><span class="sxs-lookup"><span data-stu-id="49a54-132">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="49a54-133">Таким образом нет toopay для неактивных виртуальных машин и отсутствии tooreserve ресурсов, заранее.</span><span class="sxs-lookup"><span data-stu-id="49a54-133">So, you don't have toopay for idle VMs, and you don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="49a54-134">toolearn Дополнительные сведения о планах размещения см [планы потребления функций Azure и службы приложений](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="49a54-134">toolearn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="49a54-135">Образец шаблона диспетчера ресурсов Azure см. на странице [Function app on Consumption plan] (План потребления приложения-функции)</span><span class="sxs-lookup"><span data-stu-id="49a54-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="49a54-136">Создание плана потребления</span><span class="sxs-lookup"><span data-stu-id="49a54-136">Create a Consumption plan</span></span>

<span data-ttu-id="49a54-137">План потребления — это специальный тип ресурса "ферма серверов".</span><span class="sxs-lookup"><span data-stu-id="49a54-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="49a54-138">Можно указать с помощью hello `Dynamic` значение hello `computeMode` и `sku` свойства:</span><span class="sxs-lookup"><span data-stu-id="49a54-138">You specify it by using hello `Dynamic` value for hello `computeMode` and `sku` properties:</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="49a54-139">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="49a54-139">Create a function app</span></span>

<span data-ttu-id="49a54-140">Кроме того, план потребления требует двух дополнительных настроек в конфигурации сайта hello: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` и `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="49a54-140">In addition, a Consumption plan requires two additional settings in hello site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="49a54-141">Эти свойства позволяют настраивать hello хранилища учетной записи и путь к файлу хранения код приложения функции hello и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="49a54-141">These properties configure hello storage account and file path where hello function app code and configuration are stored.</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a><span data-ttu-id="49a54-142">Развертывание приложения функции на hello план служб приложений</span><span class="sxs-lookup"><span data-stu-id="49a54-142">Deploy a function app on hello App Service plan</span></span>

<span data-ttu-id="49a54-143">В hello план служб приложений функция приложения выполняется на выделенных виртуальных машинах на Basic, Standard и Premium SKU, аналогичные tooweb приложений.</span><span class="sxs-lookup"><span data-stu-id="49a54-143">In hello App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooweb apps.</span></span> <span data-ttu-id="49a54-144">Дополнительные сведения о работе hello план служб приложений см. в разделе hello [исчерпывающий обзор планы службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49a54-144">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="49a54-145">Образец шаблона Azure Resource Manager см. на странице [Function app on Azure App Service plan] (Приложение-функция в плане службы приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="49a54-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="49a54-146">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="49a54-146">Create an App Service plan</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="49a54-147">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="49a54-147">Create a function app</span></span> 

<span data-ttu-id="49a54-148">Выбрав вариант масштабирования, создайте приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="49a54-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="49a54-149">приложение Hello — hello контейнер, который содержит все функции.</span><span class="sxs-lookup"><span data-stu-id="49a54-149">hello app is hello container that holds all your functions.</span></span>

<span data-ttu-id="49a54-150">Приложение-функция содержит много дочерних ресурсов, которые можно использовать при развертывании, в том числе параметры приложения и параметры системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="49a54-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="49a54-151">Можно также выбрать tooremove hello **sourcecontrols** дочерний ресурс и используйте другой [вариант развертывания](functions-continuous-deployment.md) вместо него.</span><span class="sxs-lookup"><span data-stu-id="49a54-151">You also might choose tooremove hello **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49a54-152">toosuccessfully развернуть приложение с помощью диспетчера ресурсов Azure, важно toounderstand способа развертывания ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="49a54-152">toosuccessfully deploy your application by using Azure Resource Manager, it's important toounderstand how resources are deployed in Azure.</span></span> <span data-ttu-id="49a54-153">В следующем примере hello, верхнего уровня конфигурации применяются с помощью **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="49a54-153">In hello following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="49a54-154">Это важные tooset этих конфигураций на высшем уровне, так как они передают сведения toohello функции среды выполнения и развертывания ядра.</span><span class="sxs-lookup"><span data-stu-id="49a54-154">It's important tooset these configurations at a top level, because they convey information toohello Functions runtime and deployment engine.</span></span> <span data-ttu-id="49a54-155">Необходимы сведения верхнего уровня перед дочерним элементом hello **sourcecontrols и веб-** применяется ресурсов.</span><span class="sxs-lookup"><span data-stu-id="49a54-155">Top-level information is required before hello child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="49a54-156">Несмотря на возможные tooconfigure эти параметры в hello дочернего уровня **config/appSettings** ресурсов, в некоторых случаях функции приложения должны быть развернуты *перед* **config/appSettings**  применяется.</span><span class="sxs-lookup"><span data-stu-id="49a54-156">Although it's possible tooconfigure these settings in hello child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="49a54-157">В таких случаях, например в [Logic Apps](../logic-apps/index.md), функции зависят от другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="49a54-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> <span data-ttu-id="49a54-158">Этот шаблон использует hello [проекта](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) значение параметров приложения, которое задает hello базовый каталог, в какой hello подсистема развертывания функции (Kudu) ищет развертываемых код.</span><span class="sxs-lookup"><span data-stu-id="49a54-158">This template uses hello [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets hello base directory in which hello Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="49a54-159">В нашем репозитории нашей функции находятся в вложенную Привет **src** папки.</span><span class="sxs-lookup"><span data-stu-id="49a54-159">In our repository, our functions are in a subfolder of hello **src** folder.</span></span> <span data-ttu-id="49a54-160">Таким образом, в предыдущих пример hello, задается значение параметров приложения hello слишком`src`.</span><span class="sxs-lookup"><span data-stu-id="49a54-160">So, in hello preceding example, we set hello app settings value too`src`.</span></span> <span data-ttu-id="49a54-161">Если функций находятся в корне hello репозиторий или не выполняется развертывание из системы управления версиями, можно удалить это значение параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="49a54-161">If your functions are in hello root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="49a54-162">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="49a54-162">Deploy your template</span></span>

<span data-ttu-id="49a54-163">Можно использовать любой из следующих способов toodeploy hello шаблон:</span><span class="sxs-lookup"><span data-stu-id="49a54-163">You can use any of hello following ways toodeploy your template:</span></span>

* [<span data-ttu-id="49a54-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49a54-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="49a54-165">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="49a54-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="49a54-166">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="49a54-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="49a54-167">REST API</span><span class="sxs-lookup"><span data-stu-id="49a54-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a><span data-ttu-id="49a54-168">TooAzure кнопка "Развертывание"</span><span class="sxs-lookup"><span data-stu-id="49a54-168">Deploy tooAzure button</span></span>

<span data-ttu-id="49a54-169">Замените ```<url-encoded-path-to-azuredeploy-json>``` с [URL-адреса](https://www.bing.com/search?q=url+encode) версии hello необработанный путь к `azuredeploy.json` в GitHub в файл.</span><span class="sxs-lookup"><span data-stu-id="49a54-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of hello raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="49a54-170">Ниже приведен пример использования разметки:</span><span class="sxs-lookup"><span data-stu-id="49a54-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="49a54-171">Ниже приведен пример использования HTML:</span><span class="sxs-lookup"><span data-stu-id="49a54-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="49a54-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="49a54-172">Next steps</span></span>

<span data-ttu-id="49a54-173">Дополнительные сведения о toodevelop и настройки функций Azure.</span><span class="sxs-lookup"><span data-stu-id="49a54-173">Learn more about how toodevelop and configure Azure Functions.</span></span>

* [<span data-ttu-id="49a54-174">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="49a54-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="49a54-175">Как tooconfigure Azure функция параметров приложения</span><span class="sxs-lookup"><span data-stu-id="49a54-175">How tooconfigure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="49a54-176">Создание первой функции Azure</span><span class="sxs-lookup"><span data-stu-id="49a54-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[Function app on Consumption plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json (Приложение-функция в плане потребления)
[Function app on Azure App Service plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json (Приложение-функция в плане службы приложений Azure)
