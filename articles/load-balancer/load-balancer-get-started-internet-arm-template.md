---
title: "Создание доступной в Интернете внутренней подсистемы балансировки нагрузки с помощью шаблона Azure | Документация Майкрософт"
description: "Узнайте, как создать балансировщик нагрузки для Интернета в диспетчере ресурсов с помощью шаблона"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d829000e63515814b192f3f8256e3b8637bb3a34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="e206e-103">Создание балансировщика нагрузки для Интернета с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="e206e-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e206e-104">Портал</span><span class="sxs-lookup"><span data-stu-id="e206e-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="e206e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e206e-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="e206e-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="e206e-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="e206e-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="e206e-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="e206e-108">В этой статье описывается модель развертывания с использованием менеджера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e206e-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="e206e-109">Вы также можете [узнать, как создать балансировщик нагрузки для Интернета, используя классическую модель развертывания](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e206e-109">You can also [Learn how to create an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="e206e-110">Развертывание шаблона с помощью кнопки развертывания</span><span class="sxs-lookup"><span data-stu-id="e206e-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="e206e-111">Образец шаблона, который находится в общедоступном репозитории, использует файл параметров, содержащий значения по умолчанию для создания описанного выше сценария.</span><span class="sxs-lookup"><span data-stu-id="e206e-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="e206e-112">Чтобы развернуть этот шаблон, перейдите по [данной ссылке](http://go.microsoft.com/fwlink/?LinkId=544801), нажмите **Deploy to Azure**(Развернуть в Azure), при необходимости замените значения параметров по умолчанию и следуйте указаниям на портале.</span><span class="sxs-lookup"><span data-stu-id="e206e-112">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="e206e-113">Развертывание шаблона с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e206e-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="e206e-114">Чтобы развернуть шаблон, загруженный с помощью PowerShell, выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="e206e-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="e206e-115">Если вы ранее не использовали Azure PowerShell, следуйте указаниям в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview) до этапа входа в Azure и выбора подписки.</span><span class="sxs-lookup"><span data-stu-id="e206e-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="e206e-116">Выполните командлет **New-AzureRmResourceGroupDeployment** , чтобы создать группу ресурсов с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="e206e-116">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="e206e-117">Развертывание шаблона с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="e206e-117">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="e206e-118">Чтобы развернуть шаблон с помощью интерфейса командной строки Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e206e-118">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="e206e-119">Если вы еще не пользовались Azure CLI, ознакомьтесь со статьей [Установка и настройка CLI Azure](../cli-install-nodejs.md) и следуйте инструкциям вплоть до выбора учетной записи Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="e206e-119">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="e206e-120">Выполните команду **azure config mode** , чтобы переключиться в режим диспетчера ресурсов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e206e-120">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="e206e-121">Вот результат, ожидаемый для указанной выше команды:</span><span class="sxs-lookup"><span data-stu-id="e206e-121">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="e206e-122">В браузере перейдите к [шаблону быстрого запуска](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), скопируйте содержимое JSON-файла и вставьте его в новый файл на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="e206e-122">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span></span> <span data-ttu-id="e206e-123">В данном сценарии скопируйте указанные ниже значения в файл **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="e206e-123">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="e206e-124">Выполните командлет **azure group deployment create** , чтобы развернуть новый балансировщик нагрузки с помощью данного шаблона и файлов параметров, которые вы скачали и изменили ранее.</span><span class="sxs-lookup"><span data-stu-id="e206e-124">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="e206e-125">В списке, который откроется после выполнения команды, будут указаны используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="e206e-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="e206e-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e206e-126">Next steps</span></span>

[<span data-ttu-id="e206e-127">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e206e-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="e206e-128">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e206e-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="e206e-129">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e206e-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
