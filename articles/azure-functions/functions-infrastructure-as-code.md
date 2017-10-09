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
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a>Автоматизация развертывания ресурсов приложения-функции для службы "Функции Azure"

Можно использовать toodeploy шаблона диспетчера ресурсов Azure приложения функции. В этой статье рассматриваются hello необходимые ресурсы и параметры для этого. Могут потребоваться дополнительные ресурсы toodeploy, в зависимости от hello [триггеры и привязки](functions-triggers-bindings.md) в приложении функции.

Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Примеры шаблонов см. в следующих статьях:
- [Function app on Consumption plan] (Приложение-функция в плане потребления);
- [Function app on Azure App Service plan] (Приложение-функция в плане службы приложений Azure).

## <a name="required-resources"></a>Необходимые ресурсы

Для приложения-функции требуются следующие ресурсы:

* [Учетная запись хранения Azure.](../storage/index.md)
* План размещения (план потребления или план службы приложений).
* Приложение-функция. 

### <a name="storage-account"></a>Учетная запись хранения

Учетная запись хранения Azure — обязательный ресурс для приложения-функции. Необходима учетная запись общего назначения, поддерживающая большие двоичные объекты, таблицы, очереди и файлы. Дополнительные сведения см. в разделе [Требования к учетной записи хранения](functions-create-function-app-portal.md#storage-account-requirements).

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

Кроме того, hello свойства `AzureWebJobsStorage` и `AzureWebJobsDashboard` должен быть указан как параметры приложения в конфигурации сайта hello. Среда выполнения Azure функции Hello использует hello `AzureWebJobsStorage` внутренние очереди toocreate строка соединения. Здравствуйте, строка подключения `AzureWebJobsDashboard` — используется toolog tooAzure таблиц хранения и управления питанием hello **монитор** вкладка на портале hello.

Эти свойства задаются в hello `appSettings` коллекции в hello `siteConfig` объекта:

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

### <a name="hosting-plan"></a>План размещения

Определение Hello hello план размещения зависит от, используется ли план потребления или службы приложений. В разделе [развертывание приложения функции hello потребления плана](#consumption) и [развертывание приложения функции на hello план служб приложений](#app-service-plan).

### <a name="function-app"></a>Приложение-функция

ресурс приложения Hello функций определяется с помощью ресурса типа **Microsoft.Web/Site** и вид **functionapp**:

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

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a>Развертывание приложения в плане использования hello функции

Вы можете запустить приложение функции в двух разных режимах: hello потребления план и hello план служб приложений. план потребления Hello автоматически размещает вычислительной мощности, когда кода выполняется, при необходимости toohandle загрузки масштабируемостью и затем масштабируется, если код не выполняется. Таким образом нет toopay для неактивных виртуальных машин и отсутствии tooreserve ресурсов, заранее. toolearn Дополнительные сведения о планах размещения см [планы потребления функций Azure и службы приложений](functions-scale.md).

Образец шаблона диспетчера ресурсов Azure см. на странице [Function app on Consumption plan] (План потребления приложения-функции)

### <a name="create-a-consumption-plan"></a>Создание плана потребления

План потребления — это специальный тип ресурса "ферма серверов". Можно указать с помощью hello `Dynamic` значение hello `computeMode` и `sku` свойства:

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

### <a name="create-a-function-app"></a>Создание приложения-функции

Кроме того, план потребления требует двух дополнительных настроек в конфигурации сайта hello: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` и `WEBSITE_CONTENTSHARE`. Эти свойства позволяют настраивать hello хранилища учетной записи и путь к файлу хранения код приложения функции hello и конфигурации.

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

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a>Развертывание приложения функции на hello план служб приложений

В hello план служб приложений функция приложения выполняется на выделенных виртуальных машинах на Basic, Standard и Premium SKU, аналогичные tooweb приложений. Дополнительные сведения о работе hello план служб приложений см. в разделе hello [исчерпывающий обзор планы службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Образец шаблона Azure Resource Manager см. на странице [Function app on Azure App Service plan] (Приложение-функция в плане службы приложений Azure).

### <a name="create-an-app-service-plan"></a>Создание плана службы приложений

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

### <a name="create-a-function-app"></a>Создание приложения-функции 

Выбрав вариант масштабирования, создайте приложение-функцию. приложение Hello — hello контейнер, который содержит все функции.

Приложение-функция содержит много дочерних ресурсов, которые можно использовать при развертывании, в том числе параметры приложения и параметры системы управления версиями. Можно также выбрать tooremove hello **sourcecontrols** дочерний ресурс и используйте другой [вариант развертывания](functions-continuous-deployment.md) вместо него.

> [!IMPORTANT]
> toosuccessfully развернуть приложение с помощью диспетчера ресурсов Azure, важно toounderstand способа развертывания ресурсов в Azure. В следующем примере hello, верхнего уровня конфигурации применяются с помощью **siteConfig**. Это важные tooset этих конфигураций на высшем уровне, так как они передают сведения toohello функции среды выполнения и развертывания ядра. Необходимы сведения верхнего уровня перед дочерним элементом hello **sourcecontrols и веб-** применяется ресурсов. Несмотря на возможные tooconfigure эти параметры в hello дочернего уровня **config/appSettings** ресурсов, в некоторых случаях функции приложения должны быть развернуты *перед* **config/appSettings**  применяется. В таких случаях, например в [Logic Apps](../logic-apps/index.md), функции зависят от другого ресурса.

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
> Этот шаблон использует hello [проекта](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) значение параметров приложения, которое задает hello базовый каталог, в какой hello подсистема развертывания функции (Kudu) ищет развертываемых код. В нашем репозитории нашей функции находятся в вложенную Привет **src** папки. Таким образом, в предыдущих пример hello, задается значение параметров приложения hello слишком`src`. Если функций находятся в корне hello репозиторий или не выполняется развертывание из системы управления версиями, можно удалить это значение параметров приложения.

## <a name="deploy-your-template"></a>Развертывание шаблона

Можно использовать любой из следующих способов toodeploy hello шаблон:

* [PowerShell](../azure-resource-manager/resource-group-template-deploy.md)
* [Интерфейс командной строки Azure](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [Портал Azure](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [REST API](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a>TooAzure кнопка "Развертывание"

Замените ```<url-encoded-path-to-azuredeploy-json>``` с [URL-адреса](https://www.bing.com/search?q=url+encode) версии hello необработанный путь к `azuredeploy.json` в GitHub в файл.

Ниже приведен пример использования разметки:

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

Ниже приведен пример использования HTML:

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о toodevelop и настройки функций Azure.

* [Справочник разработчика по функциям Azure](functions-reference.md)
* [Как tooconfigure Azure функция параметров приложения](functions-how-to-use-azure-function-app-settings.md)
* [Создание первой функции Azure](functions-create-first-azure-function.md)

<!-- LINKS -->

[Function app on Consumption plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json (Приложение-функция в плане потребления)
[Function app on Azure App Service plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json (Приложение-функция в плане службы приложений Azure)
