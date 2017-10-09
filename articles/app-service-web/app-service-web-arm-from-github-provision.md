---
title: "aaaDeploy веб-приложения, связанные репозитории GitHub tooa | Документы Microsoft"
description: "Используйте toodeploy шаблона диспетчера ресурсов Azure веб-приложения, которое содержит проект из репозитория GitHub."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a>Развертывание репозиторий GitHub tooa связанного приложения web
В этом разделе вы узнаете, как toocreate шаблона Azure Resource Manager, которая развертывает веб-приложения, связанный проект tooa в репозитории GitHub. Вы узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello. Этот шаблон используется для собственных развертывания или настройте его toomeet вашим требованиям.

Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Полный шаблон hello, см. [Web App связанного шаблона tooGitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>Что именно развертывается
С помощью этого шаблона нужно развернуть веб-приложение, содержащее код hello из проекта в GitHub.

toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:

[![Развертывание tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>Параметры
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
URL-адрес Hello репозитории GitHub, содержащий toodeploy проекта hello. Этот параметр содержит значение по умолчанию, но это значение является только предполагаемым tooshow вы как tooprovide hello URL-адреса для репозитория. Это значение можно использовать при тестировании hello шаблона, но будете tooprovide hello URL-адрес собственный репозиторий при работе с шаблоном hello.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>ветвь
ветвь Hello hello toouse репозитория при развертывании приложения hello. значение по умолчанию Hello master, но можно указать имя hello все ветви в репозитории hello обратиться в toodeploy.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a>Toodeploy ресурсы
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>Веб-приложение
Создает веб-приложение hello связанного toohello проекта в GitHub. 

Укажите имя веб-приложения hello через hello hello **siteName** параметр и расположение hello hello веб-приложения через hello **siteLocation** параметра. В hello **dependsOn** элемент hello шаблон определяет веб-приложения hello как зависит от службы hello плана размещения. Так как он зависит от плана размещения hello, веб-приложения hello не создается, пока план размещения hello завершено. Hello **dependsOn** элементом является только используемые toospecify порядок развертывания. Если пользователь не помечает hello веб-приложения как зависимость от плана размещения hello, диспетчер ресурсов Azure попытается toocreate оба ресурса в hello одинаковое время и может возникнуть ошибка hello веб-приложения, созданный до hello плана размещения.

веб-приложения Hello также имеет дочерний ресурс, который определен в **ресурсов** разделе ниже. Этот дочерний ресурс определяет системы управления версиями для проекта hello, развернутых с помощью веб-приложения hello. В этом шаблоне hello системы управления версиями — связанного tooa конкретный репозиторий GitHub. репозитории GitHub Hello определяется кодом hello **«RepoUrl»: «https://github.com/davidebbo-test/Mvc52Application.git»** может URL-адрес репозитория hello жестко при необходимости toocreate шаблон, который развертывает несколько раз один проект, при этом не hello минимальное количество параметров.
Вместо жестко запрограммированного Здравствуйте URL-адрес репозитория, можно добавить параметр для URL-адрес репозитория hello и использовать это значение для hello **RepoUrl** свойство.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a>Команды toorun развертывания
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Инфраструктура CLI Azure

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>Azure CLI 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Содержимое JSON-файл параметров hello, см. [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

