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
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a><span data-ttu-id="b6701-103">Развертывание репозиторий GitHub tooa связанного приложения web</span><span class="sxs-lookup"><span data-stu-id="b6701-103">Deploy a web app linked tooa GitHub repository</span></span>
<span data-ttu-id="b6701-104">В этом разделе вы узнаете, как toocreate шаблона Azure Resource Manager, которая развертывает веб-приложения, связанный проект tooa в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="b6701-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app that is linked tooa project in a GitHub repository.</span></span> <span data-ttu-id="b6701-105">Вы узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="b6701-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="b6701-106">Этот шаблон используется для собственных развертывания или настройте его toomeet вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="b6701-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="b6701-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b6701-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b6701-108">Полный шаблон hello, см. [Web App связанного шаблона tooGitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b6701-108">For hello complete template, see [Web App Linked tooGitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="b6701-109">Что именно развертывается</span><span class="sxs-lookup"><span data-stu-id="b6701-109">What you will deploy</span></span>
<span data-ttu-id="b6701-110">С помощью этого шаблона нужно развернуть веб-приложение, содержащее код hello из проекта в GitHub.</span><span class="sxs-lookup"><span data-stu-id="b6701-110">With this template, you will deploy a web app that contains hello code from a project in GitHub.</span></span>

<span data-ttu-id="b6701-111">toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="b6701-111">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="b6701-112">[![Развертывание tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b6701-112">[![Deploy tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="b6701-113">Параметры</span><span class="sxs-lookup"><span data-stu-id="b6701-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="b6701-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="b6701-114">repoURL</span></span>
<span data-ttu-id="b6701-115">URL-адрес Hello репозитории GitHub, содержащий toodeploy проекта hello.</span><span class="sxs-lookup"><span data-stu-id="b6701-115">hello URL for GitHub repository that contains hello project toodeploy.</span></span> <span data-ttu-id="b6701-116">Этот параметр содержит значение по умолчанию, но это значение является только предполагаемым tooshow вы как tooprovide hello URL-адреса для репозитория.</span><span class="sxs-lookup"><span data-stu-id="b6701-116">This parameter contains a default value but this value is only intended tooshow you how tooprovide hello URL for repository.</span></span> <span data-ttu-id="b6701-117">Это значение можно использовать при тестировании hello шаблона, но будете tooprovide hello URL-адрес собственный репозиторий при работе с шаблоном hello.</span><span class="sxs-lookup"><span data-stu-id="b6701-117">You can use this value when testing hello template but you will want tooprovide hello URL your own repository when working with hello template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="b6701-118">ветвь</span><span class="sxs-lookup"><span data-stu-id="b6701-118">branch</span></span>
<span data-ttu-id="b6701-119">ветвь Hello hello toouse репозитория при развертывании приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b6701-119">hello branch of hello repository toouse when deploying hello application.</span></span> <span data-ttu-id="b6701-120">значение по умолчанию Hello master, но можно указать имя hello все ветви в репозитории hello обратиться в toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b6701-120">hello default value is master, but you can provide hello name of any branch in hello repository that you wish toodeploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="b6701-121">Toodeploy ресурсы</span><span class="sxs-lookup"><span data-stu-id="b6701-121">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="b6701-122">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="b6701-122">Web app</span></span>
<span data-ttu-id="b6701-123">Создает веб-приложение hello связанного toohello проекта в GitHub.</span><span class="sxs-lookup"><span data-stu-id="b6701-123">Creates hello web app that is linked toohello project in GitHub.</span></span> 

<span data-ttu-id="b6701-124">Укажите имя веб-приложения hello через hello hello **siteName** параметр и расположение hello hello веб-приложения через hello **siteLocation** параметра.</span><span class="sxs-lookup"><span data-stu-id="b6701-124">You specify hello name of hello web app through hello **siteName** parameter, and hello location of hello web app through hello **siteLocation** parameter.</span></span> <span data-ttu-id="b6701-125">В hello **dependsOn** элемент hello шаблон определяет веб-приложения hello как зависит от службы hello плана размещения.</span><span class="sxs-lookup"><span data-stu-id="b6701-125">In hello **dependsOn** element, hello template defines hello web app as dependent on hello service hosting plan.</span></span> <span data-ttu-id="b6701-126">Так как он зависит от плана размещения hello, веб-приложения hello не создается, пока план размещения hello завершено.</span><span class="sxs-lookup"><span data-stu-id="b6701-126">Because it is dependent on hello hosting plan, hello web app is not created until hello hosting plan has finished being created.</span></span> <span data-ttu-id="b6701-127">Hello **dependsOn** элементом является только используемые toospecify порядок развертывания.</span><span class="sxs-lookup"><span data-stu-id="b6701-127">hello **dependsOn** element is only used toospecify deployment order.</span></span> <span data-ttu-id="b6701-128">Если пользователь не помечает hello веб-приложения как зависимость от плана размещения hello, диспетчер ресурсов Azure попытается toocreate оба ресурса в hello одинаковое время и может возникнуть ошибка hello веб-приложения, созданный до hello плана размещения.</span><span class="sxs-lookup"><span data-stu-id="b6701-128">If you do not mark hello web app as dependent on hello hosting plan, Azure Resource Mananger will attempt toocreate both resources at hello same time and you may receive an error if hello web app is created before hello hosting plan.</span></span>

<span data-ttu-id="b6701-129">веб-приложения Hello также имеет дочерний ресурс, который определен в **ресурсов** разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="b6701-129">hello web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="b6701-130">Этот дочерний ресурс определяет системы управления версиями для проекта hello, развернутых с помощью веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b6701-130">This child resource defines source control for hello project deployed with hello web app.</span></span> <span data-ttu-id="b6701-131">В этом шаблоне hello системы управления версиями — связанного tooa конкретный репозиторий GitHub.</span><span class="sxs-lookup"><span data-stu-id="b6701-131">In this template, hello source control is linked tooa particular GitHub repository.</span></span> <span data-ttu-id="b6701-132">репозитории GitHub Hello определяется кодом hello **«RepoUrl»: «https://github.com/davidebbo-test/Mvc52Application.git»** может URL-адрес репозитория hello жестко при необходимости toocreate шаблон, который развертывает несколько раз один проект, при этом не hello минимальное количество параметров.</span><span class="sxs-lookup"><span data-stu-id="b6701-132">hello GitHub repository is defined with hello code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code hello repository URL when you want toocreate a template that repeatedly deploys a single project while requiring hello minimum number of parameters.</span></span>
<span data-ttu-id="b6701-133">Вместо жестко запрограммированного Здравствуйте URL-адрес репозитория, можно добавить параметр для URL-адрес репозитория hello и использовать это значение для hello **RepoUrl** свойство.</span><span class="sxs-lookup"><span data-stu-id="b6701-133">Instead of hard-coding hello repository URL, you can add a parameter for hello repository URL and use that value for hello **RepoUrl** property.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="b6701-134">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="b6701-134">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="b6701-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6701-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="b6701-136">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="b6701-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="b6701-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b6701-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="b6701-138">Содержимое JSON-файл параметров hello, см. [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="b6701-138">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

