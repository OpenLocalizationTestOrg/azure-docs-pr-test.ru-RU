---
title: "с помощью шаблона Azure Resource Manager правила авторизации Service Bus aaaCreate | Документы Microsoft"
description: "Создание правила авторизации служебной шины для пространства имен и очереди с помощью шаблона диспетчера ресурсов Azure"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="2db07-103">Создание правила авторизации служебной шины для пространства имен и очереди с помощью шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="2db07-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="2db07-104">В этой статье показано, как toouse шаблона диспетчера ресурсов Azure, создает [правила авторизации](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) для пространства имен шины обслуживания и очереди.</span><span class="sxs-lookup"><span data-stu-id="2db07-104">This article shows how toouse an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="2db07-105">Вы узнаете, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="2db07-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="2db07-106">Этот шаблон используется для собственных развертывания или настройте его toomeet вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="2db07-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="2db07-107">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="2db07-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="2db07-108">Полный шаблон hello, в разделе hello [шаблона правила авторизации Service Bus] [ Service Bus auth rule template] на GitHub.</span><span class="sxs-lookup"><span data-stu-id="2db07-108">For hello complete template, see hello [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="2db07-109">следующие шаблоны Azure Resource Manager Hello доступны для загрузки и развертывания.</span><span class="sxs-lookup"><span data-stu-id="2db07-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="2db07-110">Создайте пространство имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="2db07-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="2db07-111">Создание пространства имен служебной шины с очередью</span><span class="sxs-lookup"><span data-stu-id="2db07-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="2db07-112">Создание пространства имен служебной шины с разделом и подпиской</span><span class="sxs-lookup"><span data-stu-id="2db07-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="2db07-113">Создание пространства имен служебной шины с разделом, подпиской и правилом с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2db07-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="2db07-114">toocheck для hello последние шаблоны, посетите hello [шаблоны быстрый запуск Azure] [ Azure Quickstart Templates] коллекции и выполните поиск «Шина обслуживания».</span><span class="sxs-lookup"><span data-stu-id="2db07-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="2db07-115">Что вы развернете?</span><span class="sxs-lookup"><span data-stu-id="2db07-115">What will you deploy?</span></span>
<span data-ttu-id="2db07-116">С помощью этого шаблона вы развернете правило авторизации служебной шины для пространства имен и сущности обмена сообщениями (в нашем примере — очереди).</span><span class="sxs-lookup"><span data-stu-id="2db07-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="2db07-117">Для проверки подлинности этот шаблон использует [подписанный URL-адрес (SAS)](service-bus-sas.md).</span><span class="sxs-lookup"><span data-stu-id="2db07-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="2db07-118">SAS позволяет tooService tooauthenticate приложений шины с помощью клавиши доступа, настроенной на приветствия имен или hello сущности (очереди или раздела) обмена сообщениями с связаны определенные права.</span><span class="sxs-lookup"><span data-stu-id="2db07-118">SAS enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="2db07-119">Затем можно использовать этот ключа toogenerate маркер SAS, которая tooauthenticate tooService шины в свою очередь может использоваться клиентами.</span><span class="sxs-lookup"><span data-stu-id="2db07-119">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="2db07-120">toorun hello развертывания автоматически, нажмите кнопку hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="2db07-120">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="2db07-121">[![Развертывание tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="2db07-121">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="2db07-122">Параметры</span><span class="sxs-lookup"><span data-stu-id="2db07-122">Parameters</span></span>

<span data-ttu-id="2db07-123">С помощью диспетчера ресурсов Azure можно определить параметры для значения требуется toospecify при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="2db07-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="2db07-124">шаблон Hello имеется раздел с именем `Parameters` , содержащий все значения параметров hello.</span><span class="sxs-lookup"><span data-stu-id="2db07-124">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="2db07-125">Следует определить параметр для те значения, которые будут различаться на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="2db07-125">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="2db07-126">Определяет параметры для значения, которые всегда останутся hello таким же.</span><span class="sxs-lookup"><span data-stu-id="2db07-126">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="2db07-127">Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="2db07-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="2db07-128">шаблон Hello определяет hello следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="2db07-128">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="2db07-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="2db07-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="2db07-130">Имя Hello toocreate пространство имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="2db07-130">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="2db07-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="2db07-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="2db07-132">Hello имя hello правила авторизации для пространства имен hello.</span><span class="sxs-lookup"><span data-stu-id="2db07-132">hello name of hello authorization rule for hello namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="2db07-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="2db07-133">serviceBusQueueName</span></span>
<span data-ttu-id="2db07-134">Имя Hello hello очереди в пространстве имен Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="2db07-134">hello name of hello queue in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="2db07-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="2db07-135">serviceBusApiVersion</span></span>
<span data-ttu-id="2db07-136">версия API служебной шины Hello hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="2db07-136">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="2db07-137">Toodeploy ресурсы</span><span class="sxs-lookup"><span data-stu-id="2db07-137">Resources toodeploy</span></span>
<span data-ttu-id="2db07-138">Создает стандартное пространство имен служебной шины типа **Messaging**и правило авторизации служебной шины для пространства имен и сущности.</span><span class="sxs-lookup"><span data-stu-id="2db07-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="2db07-139">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="2db07-139">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="2db07-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2db07-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="2db07-141">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="2db07-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="2db07-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2db07-142">Next steps</span></span>
<span data-ttu-id="2db07-143">Теперь, создания и развертывания ресурсов с помощью диспетчера ресурсов Azure, узнайте, как toomanage эти ресурсы в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="2db07-143">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="2db07-144">Управление служебной шиной с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="2db07-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="2db07-145">Управление ресурсами Service Bus с помощью обозревателя Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="2db07-145">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="2db07-146">Аутентификация и авторизация в служебной шине</span><span class="sxs-lookup"><span data-stu-id="2db07-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
