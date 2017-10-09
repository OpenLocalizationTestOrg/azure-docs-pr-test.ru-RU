---
title: "aaaCreate подписки раздела шины обслуживания Azure и правила с помощью шаблона Azure Resource Manager | Документы Microsoft"
description: "Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="06c35-103">Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="06c35-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="06c35-104">В этой статье показано, как toouse шаблона диспетчера ресурсов Azure, создает пространство имен служебной шины с раздела, подписки и правила (фильтр).</span><span class="sxs-lookup"><span data-stu-id="06c35-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="06c35-105">Вы узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="06c35-105">You learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="06c35-106">Этот шаблон используется для собственных развертывания или настройте его toomeet требований</span><span class="sxs-lookup"><span data-stu-id="06c35-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="06c35-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="06c35-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="06c35-108">Дополнительные сведения о практиках и шаблонах соглашений об именовании ресурсов Azure см. в разделе [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources] (Рекомендуемые соглашения об именовании ресурсов Azure).</span><span class="sxs-lookup"><span data-stu-id="06c35-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="06c35-109">Полный шаблон hello, в разделе hello [пространства имен Service Bus с раздела, подписки и правила] [ Service Bus namespace with topic, subscription, and rule] шаблона.</span><span class="sxs-lookup"><span data-stu-id="06c35-109">For hello complete template, see hello [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="06c35-110">следующие шаблоны Azure Resource Manager Hello доступны для загрузки и развертывания.</span><span class="sxs-lookup"><span data-stu-id="06c35-110">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="06c35-111">Создание пространства имен служебной шины с очередью и правилом авторизации</span><span class="sxs-lookup"><span data-stu-id="06c35-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="06c35-112">Создание пространства имен служебной шины с очередью</span><span class="sxs-lookup"><span data-stu-id="06c35-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="06c35-113">Создайте пространство имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="06c35-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="06c35-114">Создание пространства имен служебной шины с разделом и подпиской</span><span class="sxs-lookup"><span data-stu-id="06c35-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="06c35-115">toocheck для hello последние шаблоны, посетите hello [шаблоны быстрый запуск Azure] [ Azure Quickstart Templates] коллекции и выполните поиск по Service Bus.</span><span class="sxs-lookup"><span data-stu-id="06c35-115">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="06c35-116">Что вы развернете?</span><span class="sxs-lookup"><span data-stu-id="06c35-116">What will you deploy?</span></span>

<span data-ttu-id="06c35-117">С помощью этого шаблона вы развернете пространство имен служебной шины с разделом, подпиской и правилом (фильтром).</span><span class="sxs-lookup"><span data-stu-id="06c35-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="06c35-118">[Разделы и подписки служебной шины](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) предоставляют разновидность взаимодействия "один ко многим" в рамках схемы *публикации или подписки*.</span><span class="sxs-lookup"><span data-stu-id="06c35-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="06c35-119">При использовании разделов и подписок, компоненты распределенного приложения не взаимодействуют напрямую друг с другом, вместо этого они обмениваются сообщениями через раздел, в котором действует как посредник. Tooa подписки раздела напоминает виртуальную очередь, получающую копии сообщений, отправленных toohello раздела.</span><span class="sxs-lookup"><span data-stu-id="06c35-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription tooa topic resembles a virtual queue that receives copies of messages that were sent toohello topic.</span></span> <span data-ttu-id="06c35-120">Фильтр подписки позволяет toospecify сообщений отправила разделе tooa должны появиться в подписку определенного раздела.</span><span class="sxs-lookup"><span data-stu-id="06c35-120">A filter on subscription enables you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="06c35-121">Что такое правила (фильтры)?</span><span class="sxs-lookup"><span data-stu-id="06c35-121">What are rules (filters)?</span></span>

<span data-ttu-id="06c35-122">Во многих ситуациях сообщения с определенными характеристиками должны обрабатываться разными способами.</span><span class="sxs-lookup"><span data-stu-id="06c35-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="06c35-123">tooenable это, можно настроить подписки toofind сообщений, которые имеют определенные свойства, а затем выполните изменения toothose свойства.</span><span class="sxs-lookup"><span data-stu-id="06c35-123">tooenable this, you can configure subscriptions toofind messages that have specific properties and then perform modifications toothose properties.</span></span> <span data-ttu-id="06c35-124">Несмотря на то, что все сообщения, отправленные toohello разделе подписках Service Bus см можно скопировать только подмножество этих сообщений toohello виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="06c35-124">Although Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="06c35-125">Это возможно благодаря использованию фильтров подписок.</span><span class="sxs-lookup"><span data-stu-id="06c35-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="06c35-126">toolearn Дополнительные сведения о правилах (фильтры), в разделе [правила и действия](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="06c35-126">toolearn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="06c35-127">toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="06c35-127">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="06c35-128">[![Развертывание tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="06c35-128">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="06c35-129">Параметры</span><span class="sxs-lookup"><span data-stu-id="06c35-129">Parameters</span></span>

<span data-ttu-id="06c35-130">С помощью диспетчера ресурсов Azure необходимо определить параметры для значения требуется toospecify при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="06c35-130">With Azure Resource Manager, you should define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="06c35-131">шаблон Hello имеется раздел с именем `Parameters` , содержащий значения всех параметров hello.</span><span class="sxs-lookup"><span data-stu-id="06c35-131">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="06c35-132">Следует определить параметр для тех значений, которые отличаются на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="06c35-132">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="06c35-133">Определяет параметры для hello значения, которые всегда остаются одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="06c35-133">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="06c35-134">Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="06c35-134">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="06c35-135">шаблон Hello определяет hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="06c35-135">hello template defines hello following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="06c35-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="06c35-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="06c35-137">Имя Hello toocreate пространство имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="06c35-137">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="06c35-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="06c35-138">serviceBusTopicName</span></span>
<span data-ttu-id="06c35-139">Имя Hello раздел hello, создан в пространстве имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="06c35-139">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="06c35-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="06c35-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="06c35-141">Имя Hello hello подписка, созданная в пространство имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="06c35-141">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="06c35-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="06c35-142">serviceBusRuleName</span></span>
<span data-ttu-id="06c35-143">Имя Hello rule(filter) hello, созданные в пространство имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="06c35-143">hello name of hello rule(filter) created in hello Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="06c35-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="06c35-144">serviceBusApiVersion</span></span>
<span data-ttu-id="06c35-145">версия API служебной шины Hello hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="06c35-145">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="06c35-146">Toodeploy ресурсы</span><span class="sxs-lookup"><span data-stu-id="06c35-146">Resources toodeploy</span></span>
<span data-ttu-id="06c35-147">Создает стандартное пространство имен служебной шины типа **Messaging** с разделом, подпиской и правилами.</span><span class="sxs-lookup"><span data-stu-id="06c35-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
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
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="06c35-148">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="06c35-148">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="06c35-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06c35-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="06c35-150">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="06c35-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="06c35-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06c35-151">Next steps</span></span>
<span data-ttu-id="06c35-152">Теперь, создания и развертывания ресурсов с помощью диспетчера ресурсов Azure, узнайте, как toomanage эти ресурсы в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="06c35-152">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="06c35-153">Управление служебной шиной Azure</span><span class="sxs-lookup"><span data-stu-id="06c35-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="06c35-154">Управление служебной шиной с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="06c35-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="06c35-155">Управление ресурсами Service Bus с помощью обозревателя Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="06c35-155">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

