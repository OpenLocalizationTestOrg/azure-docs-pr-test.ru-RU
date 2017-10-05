---
title: "Развертывание веб-приложения, связанного с репозиторием GitHub | Документация Майкрософт"
description: "Используйте шаблон диспетчера ресурсов Azure для развертывания веб-приложения, содержащего проект из репозитория GitHub."
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
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a><span data-ttu-id="8b909-103">Развертывание веб-приложения, связанного с репозиторием GitHub</span><span class="sxs-lookup"><span data-stu-id="8b909-103">Deploy a web app linked to a GitHub repository</span></span>
<span data-ttu-id="8b909-104">В этом разделе рассказывается, как создать шаблон диспетчера ресурсов Azure, выполняющий развертывание веб-приложения, которое связано с проектом в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b909-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span></span> <span data-ttu-id="8b909-105">Вы узнаете, как определить развертываемые ресурсы и параметры, указываемые при развертывании.</span><span class="sxs-lookup"><span data-stu-id="8b909-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="8b909-106">Этот шаблон можно использовать для собственных развертываний или настроить его в соответствии с вашими требованиями.</span><span class="sxs-lookup"><span data-stu-id="8b909-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="8b909-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8b909-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="8b909-108">Полная версия шаблона приведена в файле [Веб-приложение, связанное с шаблоном GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="8b909-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="8b909-109">Что именно развертывается</span><span class="sxs-lookup"><span data-stu-id="8b909-109">What you will deploy</span></span>
<span data-ttu-id="8b909-110">С помощью этого шаблона можно развернуть веб-приложение, содержащее код проекта из GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b909-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span></span>

<span data-ttu-id="8b909-111">Чтобы выполнить развертывание автоматически, нажмите следующую кнопку.</span><span class="sxs-lookup"><span data-stu-id="8b909-111">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="8b909-112">[![Развертывание в Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8b909-112">[![Deploy to Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="8b909-113">Параметры</span><span class="sxs-lookup"><span data-stu-id="8b909-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="8b909-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="8b909-114">repoURL</span></span>
<span data-ttu-id="8b909-115">URL-адрес репозитория GitHub, в котором расположен развертываемый проект.</span><span class="sxs-lookup"><span data-stu-id="8b909-115">The URL for GitHub repository that contains the project to deploy.</span></span> <span data-ttu-id="8b909-116">Этот параметр содержит значение по умолчанию, которое лишь показывает, как указывать URL-адрес для репозитория.</span><span class="sxs-lookup"><span data-stu-id="8b909-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span></span> <span data-ttu-id="8b909-117">Это значение можно использовать при проверке шаблона, но при работе с ним вам нужно будет указать URL-адрес своего репозитория.</span><span class="sxs-lookup"><span data-stu-id="8b909-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="8b909-118">ветвь</span><span class="sxs-lookup"><span data-stu-id="8b909-118">branch</span></span>
<span data-ttu-id="8b909-119">Ветвь репозитория для развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="8b909-119">The branch of the repository to use when deploying the application.</span></span> <span data-ttu-id="8b909-120">По умолчанию указана основная ветвь, но можно указать любую другую ветвь репозитория, из которой вы хотите развернуть приложение.</span><span class="sxs-lookup"><span data-stu-id="8b909-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="8b909-121">Развертываемые ресурсы</span><span class="sxs-lookup"><span data-stu-id="8b909-121">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="8b909-122">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="8b909-122">Web app</span></span>
<span data-ttu-id="8b909-123">Создает веб-приложение, связанное с проектом в GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b909-123">Creates the web app that is linked to the project in GitHub.</span></span> 

<span data-ttu-id="8b909-124">Имя веб-приложения задается с помощью параметра **siteName**, а его расположение — с помощью параметра **siteLocation**.</span><span class="sxs-lookup"><span data-stu-id="8b909-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span></span> <span data-ttu-id="8b909-125">В элементе **dependsOn** шаблон определяет зависимость веб-приложения от плана размещения служб.</span><span class="sxs-lookup"><span data-stu-id="8b909-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span></span> <span data-ttu-id="8b909-126">Поскольку веб-приложение зависит от плана размещения, оно не создается до тех пор, пока не завершено создание плана.</span><span class="sxs-lookup"><span data-stu-id="8b909-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span></span> <span data-ttu-id="8b909-127">Элемент **dependsOn** используется только для определения последовательности развертывания.</span><span class="sxs-lookup"><span data-stu-id="8b909-127">The **dependsOn** element is only used to specify deployment order.</span></span> <span data-ttu-id="8b909-128">Если веб-приложение не пометить как зависимое от плана размещения, диспетчер ресурсов Azure попытается создать оба ресурса одновременно, в результате чего может появиться сообщение об ошибке (в случае если веб-приложение будет создано до плана размещения).</span><span class="sxs-lookup"><span data-stu-id="8b909-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span></span>

<span data-ttu-id="8b909-129">У веб-приложения также есть дочерний ресурс, определенный в разделе **resources** ниже.</span><span class="sxs-lookup"><span data-stu-id="8b909-129">The web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="8b909-130">Дочерний ресурс задает систему управления версиями для проекта, развертываемого с помощью веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8b909-130">This child resource defines source control for the project deployed with the web app.</span></span> <span data-ttu-id="8b909-131">В этом шаблоне система управления версиями связана с определенным репозиторием GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b909-131">In this template, the source control is linked to a particular GitHub repository.</span></span> <span data-ttu-id="8b909-132">Репозиторий GitHub задается с помощью кода **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"**. URL-адрес репозитория можно жестко задать, если необходимо создать шаблон, развертывающий один проект с минимальным набором параметров.</span><span class="sxs-lookup"><span data-stu-id="8b909-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span></span>
<span data-ttu-id="8b909-133">Вместо этого также можно добавить параметр URL-адреса репозитория и использовать его значение для свойства **RepoUrl**.</span><span class="sxs-lookup"><span data-stu-id="8b909-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="8b909-134">Команды для выполнения развертывания</span><span class="sxs-lookup"><span data-stu-id="8b909-134">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="8b909-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b909-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="8b909-136">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="8b909-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="8b909-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8b909-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="8b909-138">Содержимое JSON-файла параметров см. в [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="8b909-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

