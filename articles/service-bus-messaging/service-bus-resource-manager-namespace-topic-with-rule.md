---
title: "Создание подписки на раздел и правила служебной шины Azure с помощью шаблона Azure Resource Manager | Документация Майкрософт"
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
ms.openlocfilehash: 35e67d86b42358c4ce28b41beae1ee8e1896e939
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="6595f-103">Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6595f-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="6595f-104">В этой статье показывается, как использовать шаблон Azure Resource Manager, создающий пространство имен служебной шины с разделом, подпиской и правилом (фильтром).</span><span class="sxs-lookup"><span data-stu-id="6595f-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="6595f-105">Вы узнаете, как определить развертываемые ресурсы и параметры, указываемые при развертывании.</span><span class="sxs-lookup"><span data-stu-id="6595f-105">You learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="6595f-106">Этот шаблон можно использовать для собственных развертываний или изменить его в соответствии с вашими требованиями.</span><span class="sxs-lookup"><span data-stu-id="6595f-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="6595f-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="6595f-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="6595f-108">Дополнительные сведения о практиках и шаблонах соглашений об именовании ресурсов Azure см. в разделе [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources] (Рекомендуемые соглашения об именовании ресурсов Azure).</span><span class="sxs-lookup"><span data-stu-id="6595f-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="6595f-109">Полный шаблон пространства имен служебной шины с разделом, подпиской и правилом приведен [здесь][Service Bus namespace with topic, subscription, and rule].</span><span class="sxs-lookup"><span data-stu-id="6595f-109">For the complete template, see the [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="6595f-110">Для скачивания и развертывания можно использовать указанные ниже шаблоны диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="6595f-110">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="6595f-111">Создание пространства имен служебной шины с очередью и правилом авторизации</span><span class="sxs-lookup"><span data-stu-id="6595f-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="6595f-112">Создание пространства имен служебной шины с очередью</span><span class="sxs-lookup"><span data-stu-id="6595f-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="6595f-113">Создайте пространство имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="6595f-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="6595f-114">Создание пространства имен служебной шины с разделом и подпиской</span><span class="sxs-lookup"><span data-stu-id="6595f-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="6595f-115">Чтобы узнать о новых шаблонах, в коллекции [шаблонов быстрого запуска Azure][Azure Quickstart Templates] выполните поиск "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="6595f-115">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="6595f-116">Что вы развернете?</span><span class="sxs-lookup"><span data-stu-id="6595f-116">What will you deploy?</span></span>

<span data-ttu-id="6595f-117">С помощью этого шаблона вы развернете пространство имен служебной шины с разделом, подпиской и правилом (фильтром).</span><span class="sxs-lookup"><span data-stu-id="6595f-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="6595f-118">[Разделы и подписки служебной шины](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) предоставляют разновидность взаимодействия "один ко многим" в рамках схемы *публикации или подписки*.</span><span class="sxs-lookup"><span data-stu-id="6595f-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="6595f-119">При использовании разделов и подписок компоненты распределенного приложения не взаимодействуют напрямую друг с другом, а обмениваются сообщениями через раздел, который выступает в качестве посредника. Подписка на раздел напоминает виртуальную очередь, которая получает копии сообщений, отправленных в раздел.</span><span class="sxs-lookup"><span data-stu-id="6595f-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription to a topic resembles a virtual queue that receives copies of messages that were sent to the topic.</span></span> <span data-ttu-id="6595f-120">Фильтр позволяет определить, какие посылаемые в раздел сообщения должны появляться в определенной подписке на этот раздел.</span><span class="sxs-lookup"><span data-stu-id="6595f-120">A filter on subscription enables you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="6595f-121">Что такое правила (фильтры)?</span><span class="sxs-lookup"><span data-stu-id="6595f-121">What are rules (filters)?</span></span>

<span data-ttu-id="6595f-122">Во многих ситуациях сообщения с определенными характеристиками должны обрабатываться разными способами.</span><span class="sxs-lookup"><span data-stu-id="6595f-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="6595f-123">Для этого можно настроить подписки, обеспечивающие поиск сообщений с нужными свойствами, после чего можно изменить эти свойства.</span><span class="sxs-lookup"><span data-stu-id="6595f-123">To enable this, you can configure subscriptions to find messages that have specific properties and then perform modifications to those properties.</span></span> <span data-ttu-id="6595f-124">Подписки служебной шины регистрируют все сообщения, отправленные в раздел, однако в виртуальную очередь подписки можно скопировать только подмножество этих сообщений.</span><span class="sxs-lookup"><span data-stu-id="6595f-124">Although Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="6595f-125">Это возможно благодаря использованию фильтров подписок.</span><span class="sxs-lookup"><span data-stu-id="6595f-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="6595f-126">Чтобы узнать больше о правилах (фильтрах), изучите раздел [Правила и действия](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="6595f-126">To learn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="6595f-127">Чтобы выполнить развертывание автоматически, нажмите следующую кнопку.</span><span class="sxs-lookup"><span data-stu-id="6595f-127">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="6595f-128">[![Развертывание в Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="6595f-128">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="6595f-129">Параметры</span><span class="sxs-lookup"><span data-stu-id="6595f-129">Parameters</span></span>

<span data-ttu-id="6595f-130">С помощью Azure Resource Manager следует определить параметры значений, которые должны указываться на этапе развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="6595f-130">With Azure Resource Manager, you should define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="6595f-131">В шаблоне есть раздел `Parameters` , содержащий все значения параметров.</span><span class="sxs-lookup"><span data-stu-id="6595f-131">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="6595f-132">Для этих значений необходимо определить параметры, которые будут зависеть от развертываемого проекта либо от среды, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="6595f-132">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="6595f-133">Не определяйте параметры для значений, которые не меняются.</span><span class="sxs-lookup"><span data-stu-id="6595f-133">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="6595f-134">Значение каждого параметра в шаблоне определяет развертываемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6595f-134">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="6595f-135">Ниже описаны параметры, которые определяет шаблон.</span><span class="sxs-lookup"><span data-stu-id="6595f-135">The template defines the following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="6595f-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="6595f-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="6595f-137">Имя создаваемого пространства имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="6595f-137">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="6595f-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="6595f-138">serviceBusTopicName</span></span>
<span data-ttu-id="6595f-139">Имя раздела, создаваемого в пространстве имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="6595f-139">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="6595f-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="6595f-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="6595f-141">Имя подписки, создаваемой в пространстве имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="6595f-141">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="6595f-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="6595f-142">serviceBusRuleName</span></span>
<span data-ttu-id="6595f-143">Имя правила (фильтра), создаваемого в пространстве имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="6595f-143">The name of the rule(filter) created in the Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="6595f-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="6595f-144">serviceBusApiVersion</span></span>
<span data-ttu-id="6595f-145">Версия API служебной шины для шаблона.</span><span class="sxs-lookup"><span data-stu-id="6595f-145">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="6595f-146">Развертываемые ресурсы</span><span class="sxs-lookup"><span data-stu-id="6595f-146">Resources to deploy</span></span>
<span data-ttu-id="6595f-147">Создает стандартное пространство имен служебной шины типа **Messaging** с разделом, подпиской и правилами.</span><span class="sxs-lookup"><span data-stu-id="6595f-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="6595f-148">Команды для выполнения развертывания</span><span class="sxs-lookup"><span data-stu-id="6595f-148">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="6595f-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6595f-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="6595f-150">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="6595f-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="6595f-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6595f-151">Next steps</span></span>
<span data-ttu-id="6595f-152">Теперь, когда вы создали и развернули ресурсы с помощью диспетчера ресурсов Azure, узнайте, как управлять этими ресурсами, изучив следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="6595f-152">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="6595f-153">Управление служебной шиной Azure</span><span class="sxs-lookup"><span data-stu-id="6595f-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="6595f-154">Управление служебной шиной с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="6595f-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="6595f-155">Управление ресурсами служебной шины с помощью обозревателя служебной шины</span><span class="sxs-lookup"><span data-stu-id="6595f-155">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

