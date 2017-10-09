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
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="ca1c4-103">Создание приложения логики с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="ca1c4-103">Create a Logic App using a template</span></span>
<span data-ttu-id="ca1c4-104">Шаблоны предоставляют toouse быстро разные соединители внутри приложения логики.</span><span class="sxs-lookup"><span data-stu-id="ca1c4-104">Templates provide a quick way toouse different connectors within a logic app.</span></span> <span data-ttu-id="ca1c4-105">Логику приложений включает шаблоны Azure Resource Manager для toocreate приложения логики, который можно использовать toodefine бизнес-процессов.</span><span class="sxs-lookup"><span data-stu-id="ca1c4-105">Logic apps includes Azure Resource Manager templates for you toocreate a logic app that can be used toodefine business workflows.</span></span> <span data-ttu-id="ca1c4-106">Можно определить, какие ресурсы развернуты и как параметры toodefine при развертывании приложения логики.</span><span class="sxs-lookup"><span data-stu-id="ca1c4-106">You can define which resources are deployed, and how toodefine parameters when you deploy your logic app.</span></span> <span data-ttu-id="ca1c4-107">Можно использовать этот шаблон для собственных бизнес-сценариев, или настроить его toomeet вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="ca1c4-107">You can use this template for your own business scenarios, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="ca1c4-108">Дополнительные сведения о свойствах приложения hello логику в разделе [логику приложения рабочего процесса управления API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca1c4-108">For more details on hello Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="ca1c4-109">Примеры само определение hello см. в разделе [Автор приложения логики определения](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="ca1c4-109">For examples of hello definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="ca1c4-110">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ca1c4-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="ca1c4-111">Полный шаблон hello, см. [шаблон приложения логики](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ca1c4-111">For hello complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="ca1c4-112">Что будет развернуто?</span><span class="sxs-lookup"><span data-stu-id="ca1c4-112">What you deploy</span></span>
<span data-ttu-id="ca1c4-113">С помощью этого шаблона развертывается приложение логики.</span><span class="sxs-lookup"><span data-stu-id="ca1c4-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="ca1c4-114">Развертывание hello toorun автоматически, выберите hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="ca1c4-114">toorun hello deployment automatically, select hello following button:</span></span>  

<span data-ttu-id="ca1c4-115">[![Развертывание tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ca1c4-115">[![Deploy tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="ca1c4-116">Параметры</span><span class="sxs-lookup"><span data-stu-id="ca1c4-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="ca1c4-117">testUri</span><span class="sxs-lookup"><span data-stu-id="ca1c4-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a><span data-ttu-id="ca1c4-118">Toodeploy ресурсы</span><span class="sxs-lookup"><span data-stu-id="ca1c4-118">Resources toodeploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="ca1c4-119">Приложение логики</span><span class="sxs-lookup"><span data-stu-id="ca1c4-119">Logic app</span></span>
<span data-ttu-id="ca1c4-120">Создание приложения hello логики.</span><span class="sxs-lookup"><span data-stu-id="ca1c4-120">Creates hello logic app.</span></span>

<span data-ttu-id="ca1c4-121">шаблоны Hello использует значение параметра для имени приложения hello логику.</span><span class="sxs-lookup"><span data-stu-id="ca1c4-121">hello templates uses a parameter value for hello logic app name.</span></span> <span data-ttu-id="ca1c4-122">Задает расположение hello hello логику приложения toohello же расположении, что группа ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="ca1c4-122">It sets hello location of hello logic app toohello same location as hello resource group.</span></span> 

<span data-ttu-id="ca1c4-123">Это конкретное определение выполняется один раз в час, а команды ping hello в расположении, указанном в hello **testUri** параметра.</span><span class="sxs-lookup"><span data-stu-id="ca1c4-123">This particular definition runs once an hour, and pings hello location specified in hello **testUri** parameter.</span></span> 

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


## <a name="commands-toorun-deployment"></a><span data-ttu-id="ca1c4-124">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="ca1c4-124">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="ca1c4-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca1c4-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="ca1c4-126">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="ca1c4-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



