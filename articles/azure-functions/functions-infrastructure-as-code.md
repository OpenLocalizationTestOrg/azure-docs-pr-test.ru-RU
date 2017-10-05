---
title: "Автоматизация развертывания ресурсов приложения-функции для службы \"Функции Azure\" | Документация Майкрософт"
description: "Узнайте, как создать шаблон Azure Resource Manager, позволяющий развертывать приложения-функции."
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
ms.openlocfilehash: 15496e4ab2858b2aa319d53f1c438a259a3d5e49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="1ecad-104">Автоматизация развертывания ресурсов приложения-функции для службы "Функции Azure"</span><span class="sxs-lookup"><span data-stu-id="1ecad-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="1ecad-105">Для развертывания приложения-функции можно использовать шаблон Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1ecad-105">You can use an Azure Resource Manager template to deploy a function app.</span></span> <span data-ttu-id="1ecad-106">В этой статье рассматриваются необходимые для этого ресурсы и параметры.</span><span class="sxs-lookup"><span data-stu-id="1ecad-106">This article outlines the required resources and parameters for doing so.</span></span> <span data-ttu-id="1ecad-107">В зависимости от [триггеров и привязок](functions-triggers-bindings.md) в приложении-функции может потребоваться развернуть дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1ecad-107">You might need to deploy additional resources, depending on the [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="1ecad-108">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1ecad-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="1ecad-109">Примеры шаблонов см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="1ecad-109">For sample templates, see:</span></span>
- <span data-ttu-id="1ecad-110">[Function app on Consumption plan] (Приложение-функция в плане потребления);</span><span class="sxs-lookup"><span data-stu-id="1ecad-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="1ecad-111">[Function app on Azure App Service plan] (Приложение-функция в плане службы приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="1ecad-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="1ecad-112">Необходимые ресурсы</span><span class="sxs-lookup"><span data-stu-id="1ecad-112">Required resources</span></span>

<span data-ttu-id="1ecad-113">Для приложения-функции требуются следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="1ecad-113">A function app requires these resources:</span></span>

* <span data-ttu-id="1ecad-114">[Учетная запись хранения Azure.](../storage/index.md)</span><span class="sxs-lookup"><span data-stu-id="1ecad-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="1ecad-115">План размещения (план потребления или план службы приложений).</span><span class="sxs-lookup"><span data-stu-id="1ecad-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="1ecad-116">Приложение-функция.</span><span class="sxs-lookup"><span data-stu-id="1ecad-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="1ecad-117">Учетная запись хранения</span><span class="sxs-lookup"><span data-stu-id="1ecad-117">Storage account</span></span>

<span data-ttu-id="1ecad-118">Учетная запись хранения Azure — обязательный ресурс для приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="1ecad-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="1ecad-119">Необходима учетная запись общего назначения, поддерживающая большие двоичные объекты, таблицы, очереди и файлы.</span><span class="sxs-lookup"><span data-stu-id="1ecad-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="1ecad-120">Дополнительные сведения см. в разделе [Требования к учетной записи хранения](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="1ecad-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="1ecad-121">Кроме того, свойства `AzureWebJobsStorage` и `AzureWebJobsDashboard` необходимо указать как параметры приложения в конфигурации сайта.</span><span class="sxs-lookup"><span data-stu-id="1ecad-121">In addition, the properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in the site configuration.</span></span> <span data-ttu-id="1ecad-122">Чтобы создать внутренние очереди, среда выполнения службы "Функции Azure" использует строку подключения `AzureWebJobsStorage`.</span><span class="sxs-lookup"><span data-stu-id="1ecad-122">The Azure Functions runtime uses the `AzureWebJobsStorage` connection string to create internal queues.</span></span> <span data-ttu-id="1ecad-123">Строка подключения `AzureWebJobsDashboard` используется для регистрации в Хранилище таблиц Azure и обеспечения работы вкладки **Мониторинг** на портале.</span><span class="sxs-lookup"><span data-stu-id="1ecad-123">The connection string `AzureWebJobsDashboard` is used to log to Azure Table storage and power the **Monitor** tab in the portal.</span></span>

<span data-ttu-id="1ecad-124">Эти свойства задаются в коллекции `appSettings` в объекте `siteConfig`:</span><span class="sxs-lookup"><span data-stu-id="1ecad-124">These properties are specified in the `appSettings` collection in the `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="1ecad-125">План размещения</span><span class="sxs-lookup"><span data-stu-id="1ecad-125">Hosting plan</span></span>

<span data-ttu-id="1ecad-126">Определение плана размещения зависит от того, используется ли план потребления или план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="1ecad-126">The definition of the hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="1ecad-127">Дополнительные сведения см. в разделе [Развертывание приложения-функции в плане потребления](#consumption) и [Развертывание приложения-функции в плане службы приложений](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="1ecad-127">See [Deploy a function app on the Consumption plan](#consumption) and [Deploy a function app on the App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="1ecad-128">Приложение-функция</span><span class="sxs-lookup"><span data-stu-id="1ecad-128">Function app</span></span>

<span data-ttu-id="1ecad-129">Ресурс приложения-функции определяется с помощью ресурса типа **Microsoft.Web/Site** и вида **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="1ecad-129">The function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-the-consumption-plan"></a><span data-ttu-id="1ecad-130">Развертывание приложения-функции в плане потребления</span><span class="sxs-lookup"><span data-stu-id="1ecad-130">Deploy a function app on the Consumption plan</span></span>

<span data-ttu-id="1ecad-131">Вы можете запускать приложение-функцию в двух разных режимах: план потребления и план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="1ecad-131">You can run a function app in two different modes: the Consumption plan and the App Service plan.</span></span> <span data-ttu-id="1ecad-132">План потребления автоматически выделяет вычислительные ресурсы в процессе выполнения кода, масштабируя их в соответствии с нагрузкой и уменьшая, когда код не выполняется.</span><span class="sxs-lookup"><span data-stu-id="1ecad-132">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="1ecad-133">Таким образом, нет необходимости платить за бездействующие виртуальные машины и заранее резервировать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1ecad-133">So, you don't have to pay for idle VMs, and you don't have to reserve capacity in advance.</span></span> <span data-ttu-id="1ecad-134">Дополнительные сведения о планах размещения см. в статье [Потребление Функций Azure и планы службы приложений](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="1ecad-134">To learn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="1ecad-135">Образец шаблона диспетчера ресурсов Azure см. на странице [Function app on Consumption plan] (План потребления приложения-функции)</span><span class="sxs-lookup"><span data-stu-id="1ecad-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="1ecad-136">Создание плана потребления</span><span class="sxs-lookup"><span data-stu-id="1ecad-136">Create a Consumption plan</span></span>

<span data-ttu-id="1ecad-137">План потребления — это специальный тип ресурса "ферма серверов".</span><span class="sxs-lookup"><span data-stu-id="1ecad-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="1ecad-138">Его можно указать с помощью значения `Dynamic` для свойств `computeMode` и `sku`:</span><span class="sxs-lookup"><span data-stu-id="1ecad-138">You specify it by using the `Dynamic` value for the `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="1ecad-139">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="1ecad-139">Create a function app</span></span>

<span data-ttu-id="1ecad-140">Кроме того, для плана потребления следует выполнить две дополнительные настройки в конфигурации сайта: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` и `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="1ecad-140">In addition, a Consumption plan requires two additional settings in the site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="1ecad-141">Эти свойства настраивают учетную запись хранения и путь к файлам кода приложения-функции и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1ecad-141">These properties configure the storage account and file path where the function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-the-app-service-plan"></a><span data-ttu-id="1ecad-142">Развертывание приложения-функции в плане службы приложений</span><span class="sxs-lookup"><span data-stu-id="1ecad-142">Deploy a function app on the App Service plan</span></span>

<span data-ttu-id="1ecad-143">В плане службы приложений ваши приложения-функции запускаются на выделенных виртуальных машинах на Basic, Standard и Premium SKU аналогично веб-приложениям.</span><span class="sxs-lookup"><span data-stu-id="1ecad-143">In the App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar to web apps.</span></span> <span data-ttu-id="1ecad-144">Дополнительную информацию о том, как действует план службы приложений, см. в статье [Подробный обзор планов службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ecad-144">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="1ecad-145">Образец шаблона Azure Resource Manager см. на странице [Function app on Azure App Service plan] (Приложение-функция в плане службы приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="1ecad-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="1ecad-146">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="1ecad-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="1ecad-147">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="1ecad-147">Create a function app</span></span> 

<span data-ttu-id="1ecad-148">Выбрав вариант масштабирования, создайте приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="1ecad-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="1ecad-149">Приложение является контейнером, в котором содержатся все функции.</span><span class="sxs-lookup"><span data-stu-id="1ecad-149">The app is the container that holds all your functions.</span></span>

<span data-ttu-id="1ecad-150">Приложение-функция содержит много дочерних ресурсов, которые можно использовать при развертывании, в том числе параметры приложения и параметры системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="1ecad-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="1ecad-151">Вы можете также удалить дочерний ресурс **sourcecontrols** и выбрать другой [вариант развертывания](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="1ecad-151">You also might choose to remove the **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ecad-152">Чтобы с помощью Azure Resource Manager успешно развернуть приложение, важно понимать, каким образом ресурсы развертываются в Azure.</span><span class="sxs-lookup"><span data-stu-id="1ecad-152">To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span></span> <span data-ttu-id="1ecad-153">В следующем примере конфигурации верхнего уровня применяются с помощью **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="1ecad-153">In the following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="1ecad-154">Их важно задать на верхнем уровне, так как эти конфигурации передают сведения в среду выполнения функций и механизм развертывания.</span><span class="sxs-lookup"><span data-stu-id="1ecad-154">It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine.</span></span> <span data-ttu-id="1ecad-155">Сведения верхнего уровня требуются перед применением дочернего ресурса **sourcecontrols/web**.</span><span class="sxs-lookup"><span data-stu-id="1ecad-155">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="1ecad-156">Хотя эти параметры можно настроить в дочернем ресурсе **config/appSettings**, в некоторых сценариях приложение-функцию требуется развернуть *до* применения **config/appSettings**.</span><span class="sxs-lookup"><span data-stu-id="1ecad-156">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="1ecad-157">В таких случаях, например в [Logic Apps](../logic-apps/index.md), функции зависят от другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="1ecad-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="1ecad-158">В этом шаблоне используется значение параметров приложения [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file), задающее базовый каталог, в котором подсистема развертывания функций (Kudu) ищет развертываемый код.</span><span class="sxs-lookup"><span data-stu-id="1ecad-158">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="1ecad-159">В нашем репозитории функции находятся во вложенной папке папки **src**.</span><span class="sxs-lookup"><span data-stu-id="1ecad-159">In our repository, our functions are in a subfolder of the **src** folder.</span></span> <span data-ttu-id="1ecad-160">Таким образом, в предыдущем примере мы задаем для параметров приложения значение `src`.</span><span class="sxs-lookup"><span data-stu-id="1ecad-160">So, in the preceding example, we set the app settings value to `src`.</span></span> <span data-ttu-id="1ecad-161">Если ваши функции находятся в корневой папке репозитория, или если развертывание выполняется не из системы управления версиями, то это значение параметров приложения можно удалить.</span><span class="sxs-lookup"><span data-stu-id="1ecad-161">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="1ecad-162">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="1ecad-162">Deploy your template</span></span>

<span data-ttu-id="1ecad-163">Для развертывания шаблона можно использовать любой из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="1ecad-163">You can use any of the following ways to deploy your template:</span></span>

* [<span data-ttu-id="1ecad-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ecad-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="1ecad-165">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="1ecad-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="1ecad-166">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1ecad-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="1ecad-167">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="1ecad-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-to-azure-button"></a><span data-ttu-id="1ecad-168">Кнопка "Развертывание в Azure"</span><span class="sxs-lookup"><span data-stu-id="1ecad-168">Deploy to Azure button</span></span>

<span data-ttu-id="1ecad-169">Замените ```<url-encoded-path-to-azuredeploy-json>``` версией необработанного пути к файлу `azuredeploy.json` на сайте GitHub, указав его в формате [URL-адреса](https://www.bing.com/search?q=url+encode).</span><span class="sxs-lookup"><span data-stu-id="1ecad-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="1ecad-170">Ниже приведен пример использования разметки:</span><span class="sxs-lookup"><span data-stu-id="1ecad-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="1ecad-171">Ниже приведен пример использования HTML:</span><span class="sxs-lookup"><span data-stu-id="1ecad-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="1ecad-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ecad-172">Next steps</span></span>

<span data-ttu-id="1ecad-173">Дополнительные сведения о разработке и настройке Функций Azure:</span><span class="sxs-lookup"><span data-stu-id="1ecad-173">Learn more about how to develop and configure Azure Functions.</span></span>

* [<span data-ttu-id="1ecad-174">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="1ecad-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="1ecad-175">Управление приложением-функцией на портале Azure</span><span class="sxs-lookup"><span data-stu-id="1ecad-175">How to configure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="1ecad-176">Создание первой функции Azure</span><span class="sxs-lookup"><span data-stu-id="1ecad-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[Function app on Consumption plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json (Приложение-функция в плане потребления)
[Function app on Azure App Service plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json (Приложение-функция в плане службы приложений Azure)
