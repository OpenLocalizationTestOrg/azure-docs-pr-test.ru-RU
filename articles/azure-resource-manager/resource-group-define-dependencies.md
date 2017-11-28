---
title: "Настройка порядка развертывания ресурсов Azure | Документация Майкрософт"
description: "В этой статье описан способ определения зависимостей между ресурсами во время развертывания для обеспечения правильного порядка развертывания ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="6d892-103">Определение порядка развертывания ресурсов в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d892-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="6d892-104">У заданного ресурса могут быть другие ресурсы, которые должны существовать до его развертывания.</span><span class="sxs-lookup"><span data-stu-id="6d892-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="6d892-105">Например, сервер SQL Server должен существовать до развертывания базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6d892-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="6d892-106">Эта связь определяется путем пометки одного ресурса как зависимого от другого.</span><span class="sxs-lookup"><span data-stu-id="6d892-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="6d892-107">Для определения зависимостей можно использовать элемент **dependsOn** или функцию **reference**.</span><span class="sxs-lookup"><span data-stu-id="6d892-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="6d892-108">Диспетчер ресурсов оценивает зависимости между ресурсами и развертывает эти ресурсы согласно установленным зависимостям.</span><span class="sxs-lookup"><span data-stu-id="6d892-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="6d892-109">Если ресурсы не зависят друг от друга, диспетчер ресурсов развертывает их параллельно.</span><span class="sxs-lookup"><span data-stu-id="6d892-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="6d892-110">Необходимо только определить зависимости для ресурсов, которые развертываются в том же шаблоне.</span><span class="sxs-lookup"><span data-stu-id="6d892-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="6d892-111">Свойство dependsOn</span><span class="sxs-lookup"><span data-stu-id="6d892-111">dependsOn</span></span>
<span data-ttu-id="6d892-112">В шаблоне элемент dependsOn позволяет определить один ресурс как зависимый от одного или нескольких ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6d892-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="6d892-113">В качестве значения свойства может выступать список имен ресурсов с разделителями-запятыми.</span><span class="sxs-lookup"><span data-stu-id="6d892-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="6d892-114">В следующем примере показан масштабируемый набор виртуальных машин, который зависит от балансировщика нагрузки, виртуальная сеть и цикл, который создает несколько учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="6d892-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="6d892-115">Остальные ресурсы не показаны в этом примере, но они должны существовать в другом месте в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="6d892-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="6d892-116">В приведенном выше примере добавляется зависимость от ресурсов, которые создаются с помощью цикла копирования **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="6d892-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="6d892-117">Пример см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="6d892-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="6d892-118">При определении зависимостей можно указать пространство имен поставщика ресурсов и тип ресурса, чтобы избежать неоднозначности.</span><span class="sxs-lookup"><span data-stu-id="6d892-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="6d892-119">Например, чтобы уточнить сведения о подсистеме балансировки нагрузки и виртуальной сети, имена которых, возможно, совпадают с именами других ресурсов, используйте следующий формат.</span><span class="sxs-lookup"><span data-stu-id="6d892-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="6d892-120">Если вы склонны использовать свойство dependsOn для сопоставления связей между ресурсами, то вам важно понимать, зачем вы это делаете.</span><span class="sxs-lookup"><span data-stu-id="6d892-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="6d892-121">Например, для документирования связей между ресурсами использование свойства dependsOn будет неправильным решением.</span><span class="sxs-lookup"><span data-stu-id="6d892-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="6d892-122">После развертывания невозможно запросить, какие ресурсы были определены в элементе dependsOn.</span><span class="sxs-lookup"><span data-stu-id="6d892-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="6d892-123">Использование свойства dependsOn потенциально влияет на время развертывания, так как Resource Manager не может выполнять развертывание двух зависимых ресурсов параллельно.</span><span class="sxs-lookup"><span data-stu-id="6d892-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="6d892-124">Для документирования связей между ресурсами воспользуйтесь [привязкой](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="6d892-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="6d892-125">Дочерние ресурсы</span><span class="sxs-lookup"><span data-stu-id="6d892-125">Child resources</span></span>
<span data-ttu-id="6d892-126">Свойство resources позволяет указать дочерние ресурсы, связанные с определяемым ресурсом.</span><span class="sxs-lookup"><span data-stu-id="6d892-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="6d892-127">Дочерние ресурсы можно определять максимум на пяти нижестоящих уровнях.</span><span class="sxs-lookup"><span data-stu-id="6d892-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="6d892-128">Важно отметить, что неявная зависимость между дочерним и родительским ресурсами не создается.</span><span class="sxs-lookup"><span data-stu-id="6d892-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="6d892-129">Если вам нужно, чтобы дочерний ресурс был развернут после родительского ресурса, эту зависимость необходимо явно указать в свойстве dependsOn.</span><span class="sxs-lookup"><span data-stu-id="6d892-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="6d892-130">Каждый родительский ресурс принимает в качестве дочерних ресурсов только определенные типы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6d892-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="6d892-131">Принимаемые типы ресурсов указаны в [схеме шаблона](https://github.com/Azure/azure-resource-manager-schemas) родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="6d892-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="6d892-132">Имя типа дочернего ресурса содержит имя типа родительского ресурса, например: **Microsoft.Web/sites/config** и **Microsoft.Web/sites/extensions** являются дочерними ресурсами по отношению к **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="6d892-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="6d892-133">В следующем примере показаны SQL Server и база данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6d892-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="6d892-134">Обратите внимание, что несмотря на то, что база данных является дочерним ресурсом по отношению к серверу, между базой данных SQL и сервером SQL Server определена явная зависимость.</span><span class="sxs-lookup"><span data-stu-id="6d892-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="6d892-135">Функция reference</span><span class="sxs-lookup"><span data-stu-id="6d892-135">reference function</span></span>
<span data-ttu-id="6d892-136">[Функция reference](resource-group-template-functions-resource.md#reference) позволяет выражению получать его значение из других пар "имя JSON — значение" или ресурсов среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="6d892-136">The [reference function](resource-group-template-functions-resource.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="6d892-137">Выражения со ссылками неявно объявляют, что один ресурс зависит от другого.</span><span class="sxs-lookup"><span data-stu-id="6d892-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="6d892-138">Общий формат выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="6d892-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="6d892-139">В следующем примере конечная точка CDN явно зависит от профиля CDN и неявно зависит от веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6d892-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="6d892-140">Зависимости можно указать как с помощью этой функции, так и с помощью свойства dependsOn, но использовать оба варианта для одного зависимого ресурса не нужно.</span><span class="sxs-lookup"><span data-stu-id="6d892-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="6d892-141">По возможности используйте неявные ссылки, чтобы избежать добавления ненужных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="6d892-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="6d892-142">Дополнительные сведения см. в разделе о [функции reference](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="6d892-142">To learn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="6d892-143">Рекомендации по установке зависимостей</span><span class="sxs-lookup"><span data-stu-id="6d892-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="6d892-144">Решая, какие зависимости следует установить, следуйте приведенным ниже рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="6d892-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="6d892-145">Устанавливайте как можно меньше зависимостей.</span><span class="sxs-lookup"><span data-stu-id="6d892-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="6d892-146">Назначайте дочерний ресурс зависимым от его родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="6d892-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="6d892-147">Используйте функцию **reference** для задания неявных зависимостей между ресурсами, которые должны совместно использовать какое-либо свойство.</span><span class="sxs-lookup"><span data-stu-id="6d892-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="6d892-148">Не добавляйте явную зависимость (**dependsOn**), если уже определена неявная зависимость.</span><span class="sxs-lookup"><span data-stu-id="6d892-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="6d892-149">Такой подход уменьшает риск появления ненужных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="6d892-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="6d892-150">Задавайте зависимость, когда ресурс не может быть **создан** без функциональных возможностей другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="6d892-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="6d892-151">Не задавайте зависимость, если ресурсы лишь взаимодействуют после развертывания.</span><span class="sxs-lookup"><span data-stu-id="6d892-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="6d892-152">Позвольте зависимостям задействоваться последовательно, не задавая их явно.</span><span class="sxs-lookup"><span data-stu-id="6d892-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="6d892-153">Например, виртуальная машина зависит от виртуального сетевого интерфейса, а он зависит от виртуальной сети и общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="6d892-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="6d892-154">Таким образом виртуальная машина развертывается только после всех трех ресурсов, но эта зависимость виртуальной машины от них не задана явным образом.</span><span class="sxs-lookup"><span data-stu-id="6d892-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="6d892-155">Такой подход проясняет порядок зависимостей и упрощает последующее изменение шаблона.</span><span class="sxs-lookup"><span data-stu-id="6d892-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="6d892-156">Если значение может быть определено до развертывания, попробуйте развернуть ресурс без зависимостей.</span><span class="sxs-lookup"><span data-stu-id="6d892-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="6d892-157">Например, если в значении конфигурации требуется указать имя другого ресурса, можно обойтись и без зависимости.</span><span class="sxs-lookup"><span data-stu-id="6d892-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="6d892-158">Эта рекомендация не всегда уместна, так как некоторые ресурсы проверяют наличие другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="6d892-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="6d892-159">Если произошла ошибка, добавьте зависимость.</span><span class="sxs-lookup"><span data-stu-id="6d892-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="6d892-160">Resource Manager выявляет циклические зависимости во время проверки шаблона.</span><span class="sxs-lookup"><span data-stu-id="6d892-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="6d892-161">Если возникает ошибка и появляется сообщение о том, что существует циклическая зависимость, оцените шаблон на предмет лишних зависимостей, которые можно удалить.</span><span class="sxs-lookup"><span data-stu-id="6d892-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="6d892-162">Если удаление зависимостей не помогает, можно избежать появления циклических зависимостей, переместив некоторые операции развертывания в дочерние ресурсы, которые развертываются после ресурсов с циклической зависимостью.</span><span class="sxs-lookup"><span data-stu-id="6d892-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="6d892-163">Предположим, что вы развертываете две виртуальные машины, но на каждой из них необходимо задать свойства, которые ссылаются на другую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="6d892-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="6d892-164">Их можно развернуть в следующем порядке.</span><span class="sxs-lookup"><span data-stu-id="6d892-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="6d892-165">vm1.</span><span class="sxs-lookup"><span data-stu-id="6d892-165">vm1</span></span>
2. <span data-ttu-id="6d892-166">vm2.</span><span class="sxs-lookup"><span data-stu-id="6d892-166">vm2</span></span>
3. <span data-ttu-id="6d892-167">Расширение на vm1 зависит от vm1 и vm2.</span><span class="sxs-lookup"><span data-stu-id="6d892-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="6d892-168">Расширение задает на vm1 значения, получаемые от vm2.</span><span class="sxs-lookup"><span data-stu-id="6d892-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="6d892-169">Расширение на vm2 зависит от vm1 и vm2.</span><span class="sxs-lookup"><span data-stu-id="6d892-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="6d892-170">Расширение задает на vm2 значения, получаемые от vm1.</span><span class="sxs-lookup"><span data-stu-id="6d892-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="6d892-171">Сведения об оценке порядка развертывания и устранении ошибок зависимостей см. в статье [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="6d892-171">For information about assessing the deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d892-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d892-172">Next steps</span></span>
* <span data-ttu-id="6d892-173">Чтобы узнать об устранении ошибок зависимостей во время развертывания, ознакомьтесь с разделом [Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="6d892-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="6d892-174">Сведения о создании шаблонов диспетчера ресурсов Azure см. в статье о [создании шаблонов](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6d892-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="6d892-175">Список доступных в шаблоне функций см. в статье о [функциях шаблонов](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="6d892-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

