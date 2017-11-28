---
title: "Создание ресурсов служебной шины Azure с использованием шаблонов Azure Resource Manager | Документация Майкрософт"
description: "С помощью шаблонов Azure Resource Manager можно автоматизировать создание ресурсов служебной шины."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: c8142d8edfd3a527b13d655bac21acf5332f2d14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="a1073-103">Создание ресурсов служебной шины с использованием шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a1073-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="a1073-104">В этой статье описывается, как создать и развернуть ресурсы служебной шины с помощью шаблонов Azure Resource Manager, PowerShell и поставщика ресурсов служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a1073-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="a1073-105">В шаблонах Azure Resource Manager определяются ресурсы для развертывания решения и указываются параметры и переменные, позволяющие вводить значения для различных сред.</span><span class="sxs-lookup"><span data-stu-id="a1073-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="a1073-106">Шаблон состоит из JSON и выражений, на основе которых можно создавать значения для развертывания.</span><span class="sxs-lookup"><span data-stu-id="a1073-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="a1073-107">Дополнительные сведения о создании шаблонов Azure Resource Manager и описание формата шаблонов см. в статье [Описание структуры и синтаксиса шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a1073-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a1073-108">В примерах в этой статье показано, как использовать Azure Resource Manager для создания пространства имен и объекта обмена сообщениями (очереди) служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a1073-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="a1073-109">Чтобы узнать о новых шаблонах, в [коллекции шаблонов быстрого запуска Azure][Azure Quickstart Templates gallery] выполните поиск по запросу "служебная шина".</span><span class="sxs-lookup"><span data-stu-id="a1073-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="a1073-110">Шаблоны Resource Manager для служебной шины</span><span class="sxs-lookup"><span data-stu-id="a1073-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="a1073-111">Эти шаблоны Azure Resource Manager для служебной шины доступны для скачивания и развертывания.</span><span class="sxs-lookup"><span data-stu-id="a1073-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="a1073-112">Чтобы получить подробные сведения о каждом из них со ссылками на шаблоны в GitHub, щелкните приведенные ниже ссылки.</span><span class="sxs-lookup"><span data-stu-id="a1073-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="a1073-113">Создайте пространство имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="a1073-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="a1073-114">Создание пространства имен служебной шины с очередью</span><span class="sxs-lookup"><span data-stu-id="a1073-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="a1073-115">Создание пространства имен служебной шины с разделом и подпиской</span><span class="sxs-lookup"><span data-stu-id="a1073-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="a1073-116">Создание пространства имен служебной шины с очередью и правилом авторизации</span><span class="sxs-lookup"><span data-stu-id="a1073-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="a1073-117">Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a1073-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="a1073-118">Развертывание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1073-118">Deploy with PowerShell</span></span>

<span data-ttu-id="a1073-119">Ниже описывается использование PowerShell для развертывания шаблона Azure Resource Manager, который создает пространство имен служебной шины уровня **Standard** и очередь в ней.</span><span class="sxs-lookup"><span data-stu-id="a1073-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="a1073-120">Этот пример основан на шаблоне [Создание пространства имен служебной шины с очередью](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue).</span><span class="sxs-lookup"><span data-stu-id="a1073-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="a1073-121">Ниже приведена примерная последовательность действий.</span><span class="sxs-lookup"><span data-stu-id="a1073-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="a1073-122">Установите PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1073-122">Install PowerShell.</span></span>
2. <span data-ttu-id="a1073-123">Создайте шаблон и (необязательно) файл параметров.</span><span class="sxs-lookup"><span data-stu-id="a1073-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="a1073-124">В PowerShell войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a1073-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="a1073-125">Создайте группу ресурсов, если ее еще нет.</span><span class="sxs-lookup"><span data-stu-id="a1073-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="a1073-126">Протестируйте развертывание.</span><span class="sxs-lookup"><span data-stu-id="a1073-126">Test the deployment.</span></span>
6. <span data-ttu-id="a1073-127">Если необходимо, задайте режим развертывания.</span><span class="sxs-lookup"><span data-stu-id="a1073-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="a1073-128">Разверните шаблон.</span><span class="sxs-lookup"><span data-stu-id="a1073-128">Deploy the template.</span></span>

<span data-ttu-id="a1073-129">Подробные сведения о развертывании шаблонов Azure Resource Manager см. в статье [Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates] (Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a1073-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="a1073-130">Установка PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1073-130">Install PowerShell</span></span>

<span data-ttu-id="a1073-131">Установите Azure PowerShell, следуя указаниям в разделе [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps) (Приступая к работе с Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a1073-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="a1073-132">Создание шаблона</span><span class="sxs-lookup"><span data-stu-id="a1073-132">Create a template</span></span>

<span data-ttu-id="a1073-133">Клонируйте и скопируйте шаблон [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) из GitHub.</span><span class="sxs-lookup"><span data-stu-id="a1073-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="a1073-134">Создание файла параметров (необязательно)</span><span class="sxs-lookup"><span data-stu-id="a1073-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="a1073-135">Чтобы использовать необязательный файл параметров, скопируйте файл [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="a1073-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="a1073-136">Замените значение `serviceBusNamespaceName` на название пространства имен служебной шины, которое нужно создать в этом развертывании, а значение `serviceBusQueueName` — на имя очереди, которую нужно создать.</span><span class="sxs-lookup"><span data-stu-id="a1073-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

<span data-ttu-id="a1073-137">Дополнительные сведения см. в разделе [Параметры](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).</span><span class="sxs-lookup"><span data-stu-id="a1073-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="a1073-138">Вход в Azure и настройка подписки Azure</span><span class="sxs-lookup"><span data-stu-id="a1073-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="a1073-139">В командной строке PowerShell выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a1073-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="a1073-140">Вам будет предложено войти в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a1073-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="a1073-141">Войдя в систему, выполните следующую команду, чтобы просмотреть доступные подписки.</span><span class="sxs-lookup"><span data-stu-id="a1073-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="a1073-142">Эта команда возвращает список доступных подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="a1073-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="a1073-143">Выберите подписку для текущего сеанса, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="a1073-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="a1073-144">Замените `<YourSubscriptionId>` идентификатором GUID подписки Azure, которую вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="a1073-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="a1073-145">Задание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="a1073-145">Set the resource group</span></span>

<span data-ttu-id="a1073-146">Если у вас нет группы ресурсов, создайте ее с помощью команды **New-AzureRmResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="a1073-146">If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="a1073-147">Введите имя группы ресурсов и нужное расположение.</span><span class="sxs-lookup"><span data-stu-id="a1073-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="a1073-148">Например:</span><span class="sxs-lookup"><span data-stu-id="a1073-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="a1073-149">После успешного выполнения операции появится сводка по новой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a1073-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="a1073-150">тестирование развертывания</span><span class="sxs-lookup"><span data-stu-id="a1073-150">Test the deployment</span></span>

<span data-ttu-id="a1073-151">Проверьте развертывание, выполнив командлет `Test-AzureRmResourceGroupDeployment`.</span><span class="sxs-lookup"><span data-stu-id="a1073-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="a1073-152">При тестировании развернутой службы укажите точно такие же параметры, как и при ее выполнении.</span><span class="sxs-lookup"><span data-stu-id="a1073-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="a1073-153">Создание развертывания</span><span class="sxs-lookup"><span data-stu-id="a1073-153">Create the deployment</span></span>

<span data-ttu-id="a1073-154">Чтобы создать развертывание, выполните командлет `New-AzureRmResourceGroupDeployment` и укажите необходимые параметры при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="a1073-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="a1073-155">Параметры включают в себя имя развертывания, имя группы ресурсов и путь к файлу шаблона или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a1073-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="a1073-156">Если параметр **Режим** не указан, используется стандартное значение **Добавочный**.</span><span class="sxs-lookup"><span data-stu-id="a1073-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="a1073-157">Дополнительные сведения см. в статье [Добавочные и полные развертывания](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="a1073-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="a1073-158">Следующая команда запрашивает три параметра в окне PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a1073-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="a1073-159">Чтобы использовать вместо этого файл параметров, выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="a1073-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="a1073-160">При выполнении командлета развертывания также можно использовать встроенные параметры.</span><span class="sxs-lookup"><span data-stu-id="a1073-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="a1073-161">Команда выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1073-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="a1073-162">Чтобы выполнить [полное](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) развертывание, установите для параметра **Режим** значение **Полный**.</span><span class="sxs-lookup"><span data-stu-id="a1073-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="a1073-163">Проверка развертывания</span><span class="sxs-lookup"><span data-stu-id="a1073-163">Verify the deployment</span></span>
<span data-ttu-id="a1073-164">В случае успешного развертывания ресурсов в окне PowerShell будет приведена сводка по развертыванию.</span><span class="sxs-lookup"><span data-stu-id="a1073-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a><span data-ttu-id="a1073-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1073-165">Next steps</span></span>
<span data-ttu-id="a1073-166">Мы рассмотрели базовую процедуру и команды для развертывания шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a1073-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="a1073-167">Для получения более подробных сведений перейдите по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="a1073-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="a1073-168">[Общие сведения о диспетчере ресурсов Azure][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="a1073-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="a1073-169">[Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="a1073-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="a1073-170">Создание шаблонов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a1073-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
