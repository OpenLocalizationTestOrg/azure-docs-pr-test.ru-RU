---
title: "Создание приложения логики с помощью шаблона в Azure | Документация Майкрософт"
description: "Узнайте, как с помощью шаблона Azure Resource Manager развернуть приложение логики для определения рабочих процессов."
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
ms.openlocfilehash: 161adeacd6da2b15225c8a4ddae171e19e539967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="2dd3e-103">Создание приложения логики с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="2dd3e-103">Create a Logic App using a template</span></span>
<span data-ttu-id="2dd3e-104">Шаблоны предоставляют быстрый способ применения различных соединителей в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-104">Templates provide a quick way to use different connectors within a logic app.</span></span> <span data-ttu-id="2dd3e-105">Logic Apps включает в себя шаблоны Azure Resource Manager для создания приложения логики, которое можно использовать для определения бизнес-процессов.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-105">Logic apps includes Azure Resource Manager templates for you to create a logic app that can be used to define business workflows.</span></span> <span data-ttu-id="2dd3e-106">При развертывании приложения логики можно указать, какие ресурсы развертывать и как определять параметры.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-106">You can define which resources are deployed, and how to define parameters when you deploy your logic app.</span></span> <span data-ttu-id="2dd3e-107">Вы можете использовать этот шаблон для собственных бизнес-сценариев или настроить его в соответствии с вашими требованиями.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-107">You can use this template for your own business scenarios, or customize it to meet your requirements.</span></span>

<span data-ttu-id="2dd3e-108">Дополнительные сведения о свойствах приложения логики см. в статье [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx) (API управления рабочим процессом приложения логики).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-108">For more details on the Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="2dd3e-109">Примеры определения см. в статье [Создание определений приложений логики](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-109">For examples of the definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="2dd3e-110">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="2dd3e-111">Полный шаблон см. [здесь](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-111">For the complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="2dd3e-112">Что будет развернуто?</span><span class="sxs-lookup"><span data-stu-id="2dd3e-112">What you deploy</span></span>
<span data-ttu-id="2dd3e-113">С помощью этого шаблона развертывается приложение логики.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="2dd3e-114">Чтобы выполнить развертывание автоматически, нажмите следующую кнопку.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-114">To run the deployment automatically, select the following button:</span></span>  

<span data-ttu-id="2dd3e-115">[![Развертывание в Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="2dd3e-115">[![Deploy to Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="2dd3e-116">Параметры</span><span class="sxs-lookup"><span data-stu-id="2dd3e-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="2dd3e-117">testUri</span><span class="sxs-lookup"><span data-stu-id="2dd3e-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-to-deploy"></a><span data-ttu-id="2dd3e-118">Развертываемые ресурсы</span><span class="sxs-lookup"><span data-stu-id="2dd3e-118">Resources to deploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="2dd3e-119">Приложение логики</span><span class="sxs-lookup"><span data-stu-id="2dd3e-119">Logic app</span></span>
<span data-ttu-id="2dd3e-120">Создает приложение логики.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-120">Creates the logic app.</span></span>

<span data-ttu-id="2dd3e-121">В шаблонах используется значение параметра для имени приложения логики.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-121">The templates uses a parameter value for the logic app name.</span></span> <span data-ttu-id="2dd3e-122">Параметр задает в качестве расположения приложения логики то же расположение, что и у группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-122">It sets the location of the logic app to the same location as the resource group.</span></span> 

<span data-ttu-id="2dd3e-123">Это определение будет выполняться один раз в час, проверяя расположение, указанное в параметре **testUri** .</span><span class="sxs-lookup"><span data-stu-id="2dd3e-123">This particular definition runs once an hour, and pings the location specified in the **testUri** parameter.</span></span> 

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


## <a name="commands-to-run-deployment"></a><span data-ttu-id="2dd3e-124">Команды для выполнения развертывания</span><span class="sxs-lookup"><span data-stu-id="2dd3e-124">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="2dd3e-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dd3e-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="2dd3e-126">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="2dd3e-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



