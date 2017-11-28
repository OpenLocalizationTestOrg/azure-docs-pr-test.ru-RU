---
title: "aaaCreate подписки на раздел Azure Service Bus пространства имен с помощью шаблона диспетчера ресурсов Azure | Документы Microsoft"
description: "Создание пространства имен служебной шины с разделом и подпиской с помощью шаблона Azure Resource Manager."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="8e849-103">Создание пространства имен служебной шины с разделом и подпиской с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8e849-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="8e849-104">В этой статье показано, как toouse шаблона диспетчера ресурсов Azure, создает пространство имен служебной шины и раздела и подписки в этом пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="8e849-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="8e849-105">Вы узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="8e849-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="8e849-106">Этот шаблон используется для собственных развертывания или настройте его toomeet требований</span><span class="sxs-lookup"><span data-stu-id="8e849-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="8e849-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="8e849-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="8e849-108">Полный шаблон hello, в разделе hello [пространства имен Service Bus с помощью разделов и подписок] [ Service Bus namespace with topic and subscription] шаблона.</span><span class="sxs-lookup"><span data-stu-id="8e849-108">For hello complete template, see hello [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="8e849-109">следующие шаблоны Azure Resource Manager Hello доступны для загрузки и развертывания.</span><span class="sxs-lookup"><span data-stu-id="8e849-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="8e849-110">Создайте пространство имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="8e849-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="8e849-111">Создание пространства имен служебной шины с очередью</span><span class="sxs-lookup"><span data-stu-id="8e849-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="8e849-112">Создание пространства имен служебной шины с очередью и правилом авторизации</span><span class="sxs-lookup"><span data-stu-id="8e849-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="8e849-113">Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8e849-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="8e849-114">toocheck для hello последние шаблоны, посетите hello [шаблоны быстрый запуск Azure] [ Azure Quickstart Templates] коллекции и выполните поиск «Шина обслуживания».</span><span class="sxs-lookup"><span data-stu-id="8e849-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="8e849-115">Что вы развернете?</span><span class="sxs-lookup"><span data-stu-id="8e849-115">What will you deploy?</span></span>

<span data-ttu-id="8e849-116">С помощью этого шаблона вы развернете пространство имен служебной шины с разделом и подпиской.</span><span class="sxs-lookup"><span data-stu-id="8e849-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="8e849-117">[Разделы и подписки служебной шины](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) предоставляют разновидность взаимодействия "один ко многим" в рамках схемы *публикации или подписки*.</span><span class="sxs-lookup"><span data-stu-id="8e849-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="8e849-118">toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="8e849-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="8e849-119">[![Развертывание tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8e849-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="8e849-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="8e849-120">Parameters</span></span>

<span data-ttu-id="8e849-121">С помощью диспетчера ресурсов Azure можно определить параметры для значения требуется toospecify при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="8e849-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="8e849-122">шаблон Hello имеется раздел с именем `Parameters` , содержащий все значения параметров hello.</span><span class="sxs-lookup"><span data-stu-id="8e849-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="8e849-123">Следует определить параметр для те значения, которые будут различаться на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="8e849-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="8e849-124">Определяет параметры для значения, которые всегда останутся hello таким же.</span><span class="sxs-lookup"><span data-stu-id="8e849-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="8e849-125">Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="8e849-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="8e849-126">шаблон Hello определяет hello следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="8e849-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="8e849-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="8e849-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="8e849-128">Имя Hello toocreate пространство имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="8e849-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="8e849-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="8e849-129">serviceBusTopicName</span></span>
<span data-ttu-id="8e849-130">Имя Hello раздел hello, создан в пространстве имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="8e849-130">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="8e849-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="8e849-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="8e849-132">Имя Hello hello подписка, созданная в пространство имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="8e849-132">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="8e849-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="8e849-133">serviceBusApiVersion</span></span>
<span data-ttu-id="8e849-134">версия API служебной шины Hello hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="8e849-134">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="8e849-135">Toodeploy ресурсы</span><span class="sxs-lookup"><span data-stu-id="8e849-135">Resources toodeploy</span></span>
<span data-ttu-id="8e849-136">Создает стандартное пространство имен служебной шины типа **Messaging**с разделом и подпиской.</span><span class="sxs-lookup"><span data-stu-id="8e849-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="8e849-137">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="8e849-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="8e849-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e849-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="8e849-139">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="8e849-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="8e849-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8e849-140">Next steps</span></span>
<span data-ttu-id="8e849-141">Теперь, создания и развертывания ресурсов с помощью диспетчера ресурсов Azure, узнайте, как toomanage эти ресурсы в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="8e849-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="8e849-142">Управление служебной шиной с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e849-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="8e849-143">Управление ресурсами Service Bus с помощью обозревателя Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="8e849-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
