---
title: "ресурсы Azure Service Bus aaaCreate с помощью шаблонов диспетчера ресурсов Azure | Документы Microsoft"
description: "Использование диспетчера ресурсов Azure tooautomate шаблоны hello Создание ресурсов служебной шины"
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
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="407b0-103">Создание ресурсов служебной шины с использованием шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="407b0-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="407b0-104">В этой статье описывается как toocreate и развертывания ресурсов служебной шины с помощью шаблонов диспетчера ресурсов Azure, PowerShell и hello поставщика ресурсов служебной шины.</span><span class="sxs-lookup"><span data-stu-id="407b0-104">This article describes how toocreate and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and hello Service Bus resource provider.</span></span>

<span data-ttu-id="407b0-105">Шаблоны Azure Resource Manager помогает определять hello toodeploy ресурсы для решения и toospecify параметры и переменные, которые позволяют tooinput значения для различных сред.</span><span class="sxs-lookup"><span data-stu-id="407b0-105">Azure Resource Manager templates help you define hello resources toodeploy for a solution, and toospecify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="407b0-106">шаблон Hello состоит из выражения, что tooconstruct значения можно использовать для развертывания и JSON.</span><span class="sxs-lookup"><span data-stu-id="407b0-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="407b0-107">Подробные сведения о создании шаблонов диспетчера ресурсов Azure и обсуждение формата шаблона hello. в разделе [структуре и синтаксисе шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="407b0-107">For detailed information about writing Azure Resource Manager templates, and a discussion of hello template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="407b0-108">Здравствуйте, примеры в этой статье показано, как toouse Azure Resource Manager toocreate пространство имен служебной шины и обмена сообщениями (очередь) сущности.</span><span class="sxs-lookup"><span data-stu-id="407b0-108">hello examples in this article show how toouse Azure Resource Manager toocreate a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="407b0-109">Другие примеры шаблона посетите hello [коллекции шаблонов быстрый запуск Azure] [ Azure Quickstart Templates gallery] и выполните поиск «Шина обслуживания».</span><span class="sxs-lookup"><span data-stu-id="407b0-109">For other template examples, visit hello [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="407b0-110">Шаблоны Resource Manager для служебной шины</span><span class="sxs-lookup"><span data-stu-id="407b0-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="407b0-111">Эти шаблоны Azure Resource Manager для служебной шины доступны для скачивания и развертывания.</span><span class="sxs-lookup"><span data-stu-id="407b0-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="407b0-112">Щелкните hello ссылкам подробные сведения о каждой из них с помощью шаблонов toohello ссылки на GitHub:</span><span class="sxs-lookup"><span data-stu-id="407b0-112">Click hello following links for details about each one, with links toohello templates on GitHub:</span></span>

* [<span data-ttu-id="407b0-113">Создайте пространство имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="407b0-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="407b0-114">Создание пространства имен служебной шины с очередью</span><span class="sxs-lookup"><span data-stu-id="407b0-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="407b0-115">Создание пространства имен служебной шины с разделом и подпиской</span><span class="sxs-lookup"><span data-stu-id="407b0-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="407b0-116">Создание пространства имен служебной шины с очередью и правилом авторизации</span><span class="sxs-lookup"><span data-stu-id="407b0-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="407b0-117">Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="407b0-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="407b0-118">Развертывание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="407b0-118">Deploy with PowerShell</span></span>

<span data-ttu-id="407b0-119">Hello ниже описано, как toodeploy PowerShell toouse шаблона диспетчера ресурсов Azure, создает **Стандартная** уровня пространства имен шины обслуживания и очереди в этом пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="407b0-119">hello following procedure describes how toouse PowerShell toodeploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="407b0-120">Этот пример основан на hello [создание пространства имен Service Bus с очередью](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) шаблона.</span><span class="sxs-lookup"><span data-stu-id="407b0-120">This example is based on hello [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="407b0-121">Приблизительное Hello рабочий процесс выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="407b0-121">hello approximate workflow is as follows:</span></span>

1. <span data-ttu-id="407b0-122">Установите PowerShell.</span><span class="sxs-lookup"><span data-stu-id="407b0-122">Install PowerShell.</span></span>
2. <span data-ttu-id="407b0-123">Создание шаблона hello и (необязательно) файл параметров.</span><span class="sxs-lookup"><span data-stu-id="407b0-123">Create hello template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="407b0-124">В PowerShell войдите в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="407b0-124">In PowerShell, log in tooyour Azure account.</span></span>
4. <span data-ttu-id="407b0-125">Создайте группу ресурсов, если ее еще нет.</span><span class="sxs-lookup"><span data-stu-id="407b0-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="407b0-126">Тестирование развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="407b0-126">Test hello deployment.</span></span>
6. <span data-ttu-id="407b0-127">При желании установите режим развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="407b0-127">If desired, set hello deployment mode.</span></span>
7. <span data-ttu-id="407b0-128">Развертывание шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="407b0-128">Deploy hello template.</span></span>

<span data-ttu-id="407b0-129">Подробные сведения о развертывании шаблонов Azure Resource Manager см. в статье [Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates] (Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="407b0-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="407b0-130">Установка PowerShell</span><span class="sxs-lookup"><span data-stu-id="407b0-130">Install PowerShell</span></span>

<span data-ttu-id="407b0-131">Установите Azure PowerShell, следуя инструкциям hello [Приступая к работе с Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="407b0-131">Install Azure PowerShell by following hello instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="407b0-132">Создание шаблона</span><span class="sxs-lookup"><span data-stu-id="407b0-132">Create a template</span></span>

<span data-ttu-id="407b0-133">Клон или копирования hello [201-servicebus создать очередь](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) шаблона из GitHub:</span><span class="sxs-lookup"><span data-stu-id="407b0-133">Clone or copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="407b0-134">Создание файла параметров (необязательно)</span><span class="sxs-lookup"><span data-stu-id="407b0-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="407b0-135">toouse файл необязательные параметры копирования hello [201-servicebus создать очередь](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) файла.</span><span class="sxs-lookup"><span data-stu-id="407b0-135">toouse an optional parameters file, copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="407b0-136">Замените значение hello `serviceBusNamespaceName` с именем hello пространства имен Service Bus hello нужны toocreate в этом развертывании и замените значение hello `serviceBusQueueName` с именем hello hello очереди требуется toocreate.</span><span class="sxs-lookup"><span data-stu-id="407b0-136">Replace hello value of `serviceBusNamespaceName` with hello name of hello Service Bus namespace you want toocreate in this deployment, and replace hello value of `serviceBusQueueName` with hello name of hello queue you want toocreate.</span></span>

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

<span data-ttu-id="407b0-137">Дополнительные сведения см. в разделе hello [параметры](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) раздела.</span><span class="sxs-lookup"><span data-stu-id="407b0-137">For more information, see hello [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a><span data-ttu-id="407b0-138">Войдите в tooAzure и задать hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="407b0-138">Log in tooAzure and set hello Azure subscription</span></span>

<span data-ttu-id="407b0-139">В командной строке PowerShell выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="407b0-139">From a PowerShell prompt, run hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="407b0-140">Все запрашиваемые toolog на tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="407b0-140">You are prompted toolog on tooyour Azure account.</span></span> <span data-ttu-id="407b0-141">После входа в систему запустите следующие команды tooview hello доступных подписок.</span><span class="sxs-lookup"><span data-stu-id="407b0-141">After logging on, run hello following command tooview your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="407b0-142">Эта команда возвращает список доступных подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="407b0-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="407b0-143">Выберите подписку для hello текущего сеанса, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="407b0-143">Choose a subscription for hello current session by running hello following command.</span></span> <span data-ttu-id="407b0-144">Замените `<YourSubscriptionId>` hello GUID для hello подписки Azure необходимо toouse.</span><span class="sxs-lookup"><span data-stu-id="407b0-144">Replace `<YourSubscriptionId>` with hello GUID for hello Azure subscription you want toouse.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a><span data-ttu-id="407b0-145">Группа ресурсов набор hello</span><span class="sxs-lookup"><span data-stu-id="407b0-145">Set hello resource group</span></span>

<span data-ttu-id="407b0-146">Если нет существующего ресурса группы, создайте новую группу ресурсов с hello ** New AzureRmResourceGroup ** команды.</span><span class="sxs-lookup"><span data-stu-id="407b0-146">If you do not have an existing resource group, create a new resource group with hello **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="407b0-147">Укажите имя группы ресурсов hello и место toouse hello.</span><span class="sxs-lookup"><span data-stu-id="407b0-147">Provide hello name of hello resource group and location you want toouse.</span></span> <span data-ttu-id="407b0-148">Например:</span><span class="sxs-lookup"><span data-stu-id="407b0-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="407b0-149">В случае успешного выполнения отображается сводка hello новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="407b0-149">If successful, a summary of hello new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a><span data-ttu-id="407b0-150">Тестирование развертывания hello</span><span class="sxs-lookup"><span data-stu-id="407b0-150">Test hello deployment</span></span>

<span data-ttu-id="407b0-151">Проверка развертывания, выполнив hello `Test-AzureRmResourceGroupDeployment` командлета.</span><span class="sxs-lookup"><span data-stu-id="407b0-151">Validate your deployment by running hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="407b0-152">При тестировании hello развертывания, укажите параметры, точно так, как при выполнении развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="407b0-152">When testing hello deployment, provide parameters exactly as you would when executing hello deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a><span data-ttu-id="407b0-153">Создание развертывания hello</span><span class="sxs-lookup"><span data-stu-id="407b0-153">Create hello deployment</span></span>

<span data-ttu-id="407b0-154">toocreate hello новое развертывание, запустите hello `New-AzureRmResourceGroupDeployment` командлет и укажите необходимые параметры hello при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="407b0-154">toocreate hello new deployment, run hello `New-AzureRmResourceGroupDeployment` cmdlet, and provide hello necessary parameters when prompted.</span></span> <span data-ttu-id="407b0-155">Hello параметры включают имя для вашего развертывания hello имя группы ресурсов и hello путь или URL-адрес файла шаблона toohello.</span><span class="sxs-lookup"><span data-stu-id="407b0-155">hello parameters include a name for your deployment, hello name of your resource group, and hello path or URL toohello template file.</span></span> <span data-ttu-id="407b0-156">Если hello **режим** параметр не указан, значение по умолчанию hello **Incremental** используется.</span><span class="sxs-lookup"><span data-stu-id="407b0-156">If hello **Mode** parameter is not specified, hello default value of **Incremental** is used.</span></span> <span data-ttu-id="407b0-157">Дополнительные сведения см. в статье [Добавочные и полные развертывания](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="407b0-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="407b0-158">Здравствуйте, следующие командные строки вы hello трех параметров в окне PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="407b0-158">hello following command prompts you for hello three parameters in hello PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

<span data-ttu-id="407b0-159">toospecify файл параметров используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="407b0-159">toospecify a parameters file instead, use hello following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="407b0-160">Также можно использовать встроенные параметры, при запуске командлета развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="407b0-160">You can also use inline parameters when you run hello deployment cmdlet.</span></span> <span data-ttu-id="407b0-161">Команда Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="407b0-161">hello command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="407b0-162">toorun [завершения](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) развертывания, набор hello **режим** параметр слишком**завершить**:</span><span class="sxs-lookup"><span data-stu-id="407b0-162">toorun a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set hello **Mode** parameter too**Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="407b0-163">Проверка развертывания hello</span><span class="sxs-lookup"><span data-stu-id="407b0-163">Verify hello deployment</span></span>
<span data-ttu-id="407b0-164">Если ресурсы hello успешно развертывается, сводка hello развертывания отображается в окне PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="407b0-164">If hello resources are deployed successfully, a summary of hello deployment is displayed in hello PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="407b0-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="407b0-165">Next steps</span></span>
<span data-ttu-id="407b0-166">Теперь вы увидели hello базовый рабочий процесс и команды для развертывания шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="407b0-166">You've now seen hello basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="407b0-167">Для получения дополнительных сведений посетите hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="407b0-167">For more detailed information, visit hello following links:</span></span>

* <span data-ttu-id="407b0-168">[Общие сведения о диспетчере ресурсов Azure][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="407b0-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="407b0-169">[Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="407b0-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="407b0-170">Создание шаблонов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="407b0-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
