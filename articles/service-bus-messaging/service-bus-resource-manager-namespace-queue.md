---
title: "пространство имен служебной шины Azure aaaCreate и постановка в очередь с помощью шаблона диспетчера ресурсов Azure | Документы Microsoft"
description: "Создание пространства имен и очереди служебной шины с помощью шаблона диспетчера ресурсов Azure"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="c0ebb-103">Создание пространства имен и очереди служебной шины с помощью шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="c0ebb-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="c0ebb-104">В этой статье показано, как toouse шаблона диспетчера ресурсов Azure, создает пространство имен Service Bus и очереди в этом пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="c0ebb-105">Вы узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="c0ebb-106">Этот шаблон используется для собственных развертывания или настройте его toomeet вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="c0ebb-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="c0ebb-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="c0ebb-108">Полный шаблон hello, в разделе hello [шаблона пространства имен и очереди Service Bus] [ Service Bus namespace and queue template] на GitHub.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-108">For hello complete template, see hello [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="c0ebb-109">следующие шаблоны Azure Resource Manager Hello доступны для загрузки и развертывания.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="c0ebb-110">Создание пространства имен служебной шины с очередью и правилом авторизации</span><span class="sxs-lookup"><span data-stu-id="c0ebb-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="c0ebb-111">Создание пространства имен служебной шины с разделом и подпиской</span><span class="sxs-lookup"><span data-stu-id="c0ebb-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="c0ebb-112">Создайте пространство имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="c0ebb-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="c0ebb-113">Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c0ebb-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="c0ebb-114">toocheck для hello последние шаблоны, посетите hello [шаблоны быстрый запуск Azure] [ Azure Quickstart Templates] коллекции и выполните поиск «Шина обслуживания».</span><span class="sxs-lookup"><span data-stu-id="c0ebb-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="c0ebb-115">Что вы развернете?</span><span class="sxs-lookup"><span data-stu-id="c0ebb-115">What will you deploy?</span></span>

<span data-ttu-id="c0ebb-116">С помощью этого шаблона вы развернете пространство имен служебной шины с очередью.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="c0ebb-117">[Очереди шины обслуживания](service-bus-queues-topics-subscriptions.md#queues) предлагают первым пришел, tooone доставки сообщения первой Out (FIFO) или несколько конкурирующих клиентов.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery tooone or more competing consumers.</span></span>

<span data-ttu-id="c0ebb-118">toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="c0ebb-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="c0ebb-119">[![Развертывание tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="c0ebb-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="c0ebb-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="c0ebb-120">Parameters</span></span>

<span data-ttu-id="c0ebb-121">С помощью диспетчера ресурсов Azure можно определить параметры для значения требуется toospecify при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="c0ebb-122">шаблон Hello имеется раздел с именем `Parameters` , содержащий все значения параметров hello.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="c0ebb-123">Следует определить параметр для те значения, которые будут различаться на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="c0ebb-124">Определяет параметры для значения, которые всегда останутся hello таким же.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="c0ebb-125">Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="c0ebb-126">шаблон Hello определяет hello следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="c0ebb-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="c0ebb-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="c0ebb-128">Имя Hello toocreate пространство имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="c0ebb-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="c0ebb-129">serviceBusQueueName</span></span>
<span data-ttu-id="c0ebb-130">Имя очереди hello, созданной в пространстве имен Service Bus hello Hello.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-130">hello name of hello queue created in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="c0ebb-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="c0ebb-131">serviceBusApiVersion</span></span>
<span data-ttu-id="c0ebb-132">версия API служебной шины Hello hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-132">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="c0ebb-133">Toodeploy ресурсы</span><span class="sxs-lookup"><span data-stu-id="c0ebb-133">Resources toodeploy</span></span>
<span data-ttu-id="c0ebb-134">Создает стандартное пространство имен служебной шины типа **Messaging**с очередью.</span><span class="sxs-lookup"><span data-stu-id="c0ebb-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

```json
"resources ": [{
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
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="c0ebb-135">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="c0ebb-135">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="c0ebb-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0ebb-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="c0ebb-137">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="c0ebb-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="c0ebb-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0ebb-138">Next steps</span></span>
<span data-ttu-id="c0ebb-139">Теперь, создания и развертывания ресурсов с помощью диспетчера ресурсов Azure, узнайте, как toomanage эти ресурсы в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c0ebb-139">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="c0ebb-140">Управление служебной шиной с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0ebb-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="c0ebb-141">Управление ресурсами Service Bus с помощью обозревателя Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="c0ebb-141">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
