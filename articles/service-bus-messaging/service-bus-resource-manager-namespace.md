---
title: "aaaCreate пространства имен Service Bus с помощью шаблона диспетчера ресурсов Azure | Документы Microsoft"
description: "Использование шаблона Azure Resource Manager toocreate пространство имен служебной шины"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="eee01-103">Создание пространства имен служебной шины с помощью шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="eee01-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="eee01-104">В этой статье описывается, как toouse шаблона диспетчера ресурсов Azure, создает пространство имен служебной шины типа **обмен сообщениями** с номером SKU Standard и Basic.</span><span class="sxs-lookup"><span data-stu-id="eee01-104">This article describes how toouse an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="eee01-105">статья Hello также определяет hello параметры, заданные для выполнения hello hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="eee01-105">hello article also defines hello parameters that are specified for hello execution of hello deployment.</span></span> <span data-ttu-id="eee01-106">Этот шаблон используется для собственных развертывания или настройте его toomeet вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="eee01-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="eee01-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="eee01-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="eee01-108">Полный шаблон hello, в разделе hello [шаблон имен Service Bus] [ Service Bus namespace template] на GitHub.</span><span class="sxs-lookup"><span data-stu-id="eee01-108">For hello complete template, see hello [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="eee01-109">следующие шаблоны Azure Resource Manager Hello доступны для загрузки и развертывания.</span><span class="sxs-lookup"><span data-stu-id="eee01-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="eee01-110">Создание пространства имен служебной шины с очередью</span><span class="sxs-lookup"><span data-stu-id="eee01-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="eee01-111">Создание пространства имен служебной шины с разделом и подпиской</span><span class="sxs-lookup"><span data-stu-id="eee01-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="eee01-112">Создание пространства имен служебной шины с очередью и правилом авторизации</span><span class="sxs-lookup"><span data-stu-id="eee01-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="eee01-113">Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eee01-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="eee01-114">toocheck для hello последние шаблоны, посетите hello [шаблоны быстрый запуск Azure] [ Azure Quickstart Templates] коллекции и выполните поиск по Service Bus.</span><span class="sxs-lookup"><span data-stu-id="eee01-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="eee01-115">Что вы развернете?</span><span class="sxs-lookup"><span data-stu-id="eee01-115">What will you deploy?</span></span>
<span data-ttu-id="eee01-116">С помощью этого шаблона вы развернете пространство имен служебной шины с SKU уровня ["Базовый", "Стандартный" или "Премиум"](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="eee01-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="eee01-117">toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="eee01-117">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="eee01-118">[![Развертывание tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="eee01-118">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="eee01-119">Параметры</span><span class="sxs-lookup"><span data-stu-id="eee01-119">Parameters</span></span>
<span data-ttu-id="eee01-120">С помощью диспетчера ресурсов Azure можно определить параметры для значения требуется toospecify при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="eee01-120">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="eee01-121">шаблон Hello имеется раздел с именем `Parameters` , содержащий все значения параметров hello.</span><span class="sxs-lookup"><span data-stu-id="eee01-121">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="eee01-122">Следует определить параметр для те значения, которые будут различаться на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="eee01-122">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="eee01-123">Определяет параметры для значения, которые всегда останутся hello таким же.</span><span class="sxs-lookup"><span data-stu-id="eee01-123">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="eee01-124">Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="eee01-124">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="eee01-125">Этот шаблон определяет hello следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="eee01-125">This template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="eee01-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="eee01-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="eee01-127">Имя Hello toocreate пространство имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="eee01-127">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="eee01-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="eee01-128">serviceBusSKU</span></span>
<span data-ttu-id="eee01-129">Имя Hello hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span><span class="sxs-lookup"><span data-stu-id="eee01-129">hello name of hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span></span>

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="eee01-130">шаблон Hello определяет hello значения, разрешенные для этого параметра (Basic, Standard или Premium) и назначает значение по умолчанию (стандартный режим), если значение не указано.</span><span class="sxs-lookup"><span data-stu-id="eee01-130">hello template defines hello values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="eee01-131">Дополнительные сведения о ценах на использование служебной шины приведены в статье [Service Bus pricing and billing][Service Bus pricing and billing] (Сведения о расценках и выставлении счетов служебной шины).</span><span class="sxs-lookup"><span data-stu-id="eee01-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="eee01-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="eee01-132">serviceBusApiVersion</span></span>
<span data-ttu-id="eee01-133">версия API служебной шины Hello hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="eee01-133">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a><span data-ttu-id="eee01-134">Toodeploy ресурсы</span><span class="sxs-lookup"><span data-stu-id="eee01-134">Resources toodeploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="eee01-135">Пространство имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="eee01-135">Service Bus namespace</span></span>
<span data-ttu-id="eee01-136">Создает стандартное пространство имен служебной шины типа **Messaging**.</span><span class="sxs-lookup"><span data-stu-id="eee01-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="eee01-137">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="eee01-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="eee01-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eee01-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="eee01-139">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="eee01-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="eee01-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eee01-140">Next steps</span></span>
<span data-ttu-id="eee01-141">Теперь, создания и развертывания ресурсов с помощью диспетчера ресурсов Azure, узнайте, как toomanage этих ресурсов, считывая эти статьи:</span><span class="sxs-lookup"><span data-stu-id="eee01-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by reading these articles:</span></span>

* [<span data-ttu-id="eee01-142">Управление служебной шиной с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="eee01-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="eee01-143">Управление ресурсами Service Bus с помощью обозревателя Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="eee01-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
