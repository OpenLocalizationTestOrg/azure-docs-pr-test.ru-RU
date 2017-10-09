---
title: "порядок развертывания aaaSet для ресурсов Azure | Документы Microsoft"
description: "Описание способа развертывания tooset один ресурс как зависимость от другого ресурса во время развертывания tooensure ресурсы в правильном порядке hello."
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
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="4fc67-103">Задать порядок hello развертывания ресурсов в шаблоны Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4fc67-103">Define hello order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="4fc67-104">Для данного ресурса может быть другие ресурсы, которые должны существовать до развертывания ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="4fc67-104">For a given resource, there can be other resources that must exist before hello resource is deployed.</span></span> <span data-ttu-id="4fc67-105">Например SQL server должен существовать прежде чем toodeploy базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="4fc67-105">For example, a SQL server must exist before attempting toodeploy a SQL database.</span></span> <span data-ttu-id="4fc67-106">Вы определять эту связь, помечая один ресурс как зависимость от hello другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="4fc67-106">You define this relationship by marking one resource as dependent on hello other resource.</span></span> <span data-ttu-id="4fc67-107">Определение зависимостей с hello **dependsOn** элемент, или с помощью hello **ссылки** функции.</span><span class="sxs-lookup"><span data-stu-id="4fc67-107">You define a dependency with hello **dependsOn** element, or by using hello **reference** function.</span></span> 

<span data-ttu-id="4fc67-108">Диспетчер ресурсов оценивает hello зависимости между ресурсами и развертывает их в порядке зависимости.</span><span class="sxs-lookup"><span data-stu-id="4fc67-108">Resource Manager evaluates hello dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="4fc67-109">Если ресурсы не зависят друг от друга, диспетчер ресурсов развертывает их параллельно.</span><span class="sxs-lookup"><span data-stu-id="4fc67-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="4fc67-110">Требуется toodefine зависимости только для ресурсов, развернутых в hello того же шаблона.</span><span class="sxs-lookup"><span data-stu-id="4fc67-110">You only need toodefine dependencies for resources that are deployed in hello same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="4fc67-111">Свойство dependsOn</span><span class="sxs-lookup"><span data-stu-id="4fc67-111">dependsOn</span></span>
<span data-ttu-id="4fc67-112">В шаблоне элемент dependsOn hello позволяет toodefine один ресурс в зависимости от одного или нескольких ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4fc67-112">Within your template, hello dependsOn element enables you toodefine one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="4fc67-113">В качестве значения свойства может выступать список имен ресурсов с разделителями-запятыми.</span><span class="sxs-lookup"><span data-stu-id="4fc67-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="4fc67-114">Hello пример набора масштабирования виртуальных машин, который зависит от подсистемы балансировки нагрузки, виртуальной сети и цикл, который создает несколько учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="4fc67-114">hello following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="4fc67-115">Эти другие ресурсы в следующий пример hello не отображаются, но им нужны tooexist в другом месте в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="4fc67-115">These other resources are not shown in hello following example, but they would need tooexist elsewhere in hello template.</span></span>

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

<span data-ttu-id="4fc67-116">В предыдущих пример hello, зависимость включается hello ресурсов, которые создаются с помощью цикла копирования с именем **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="4fc67-116">In hello preceding example, a dependency is included on hello resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="4fc67-117">Пример см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="4fc67-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="4fc67-118">При определении зависимостей, можно включить hello ресурсов поставщика пространства имен и ресурса типа tooavoid неоднозначности.</span><span class="sxs-lookup"><span data-stu-id="4fc67-118">When defining dependencies, you can include hello resource provider namespace and resource type tooavoid ambiguity.</span></span> <span data-ttu-id="4fc67-119">Например tooclarify, балансировки нагрузки и виртуальной сети, которая может иметь hello такими же именами, как другие ресурсы hello используйте следующий формат:</span><span class="sxs-lookup"><span data-stu-id="4fc67-119">For example, tooclarify a load balancer and virtual network that may have hello same names as other resources, use hello following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="4fc67-120">Хотя может быть держите toouse dependsOn toomap связи между ресурсов, это важные toounderstand, почему вы пишете код.</span><span class="sxs-lookup"><span data-stu-id="4fc67-120">While you may be inclined toouse dependsOn toomap relationships between your resources, it's important toounderstand why you're doing it.</span></span> <span data-ttu-id="4fc67-121">Например, toodocument как ресурсы связаны между собой, dependsOn не hello правильного подхода.</span><span class="sxs-lookup"><span data-stu-id="4fc67-121">For example, toodocument how resources are interconnected, dependsOn is not hello right approach.</span></span> <span data-ttu-id="4fc67-122">Не удается запросить, какие ресурсы были определены в элементе dependsOn hello после развертывания.</span><span class="sxs-lookup"><span data-stu-id="4fc67-122">You cannot query which resources were defined in hello dependsOn element after deployment.</span></span> <span data-ttu-id="4fc67-123">Использование свойства dependsOn потенциально влияет на время развертывания, так как Resource Manager не может выполнять развертывание двух зависимых ресурсов параллельно.</span><span class="sxs-lookup"><span data-stu-id="4fc67-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="4fc67-124">toodocument связи между ресурсами, вместо этого использовать [привязке ресурсов](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="4fc67-124">toodocument relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="4fc67-125">Дочерние ресурсы</span><span class="sxs-lookup"><span data-stu-id="4fc67-125">Child resources</span></span>
<span data-ttu-id="4fc67-126">Свойства ресурсов Hello можно toospecify дочерние ресурсы, определяемый toohello связанный ресурс.</span><span class="sxs-lookup"><span data-stu-id="4fc67-126">hello resources property allows you toospecify child resources that are related toohello resource being defined.</span></span> <span data-ttu-id="4fc67-127">Дочерние ресурсы можно определять максимум на пяти нижестоящих уровнях.</span><span class="sxs-lookup"><span data-stu-id="4fc67-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="4fc67-128">Очень важно toonote, неявное зависимостей не созданы между дочерней и родительской ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="4fc67-128">It is important toonote that an implicit dependency is not created between a child resource and hello parent resource.</span></span> <span data-ttu-id="4fc67-129">Если требуется hello дочерних ресурсов toobe после hello родительский ресурс развертывание, необходимо явно указать зависимость со свойством dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="4fc67-129">If you need hello child resource toobe deployed after hello parent resource, you must explicitly state that dependency with hello dependsOn property.</span></span> 

<span data-ttu-id="4fc67-130">Каждый родительский ресурс принимает в качестве дочерних ресурсов только определенные типы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4fc67-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="4fc67-131">Hello приняты указанные типы ресурсов в hello [схема шаблона](https://github.com/Azure/azure-resource-manager-schemas) hello родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="4fc67-131">hello accepted resource types are specified in hello [template schema](https://github.com/Azure/azure-resource-manager-schemas) of hello parent resource.</span></span> <span data-ttu-id="4fc67-132">Hello имя типа ресурса дочерних содержит hello типа hello родительского ресурса, например **Microsoft.Web/sites/config** и **Microsoft.Web/sites/extensions** являются оба дочерними ресурсами hello  **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="4fc67-132">hello name of child resource type includes hello name of hello parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of hello **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="4fc67-133">Следующий пример Hello показывает SQL server и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="4fc67-133">hello following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="4fc67-134">Обратите внимание, что явных зависимостей определена между hello базы данных SQL и SQL server, несмотря на то, что hello базы данных является дочерним элементом сервера hello.</span><span class="sxs-lookup"><span data-stu-id="4fc67-134">Notice that an explicit dependency is defined between hello SQL database and SQL server, even though hello database is a child of hello server.</span></span>

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

## <a name="reference-function"></a><span data-ttu-id="4fc67-135">Функция reference</span><span class="sxs-lookup"><span data-stu-id="4fc67-135">reference function</span></span>
<span data-ttu-id="4fc67-136">Hello [ссылки на функцию](resource-group-template-functions-resource.md#reference) включает выражение tooderive свое значение из других пар имен и значений JSON или ресурсов среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="4fc67-136">hello [reference function](resource-group-template-functions-resource.md#reference) enables an expression tooderive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="4fc67-137">Выражения со ссылками неявно объявляют, что один ресурс зависит от другого.</span><span class="sxs-lookup"><span data-stu-id="4fc67-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="4fc67-138">Hello общие выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4fc67-138">hello general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="4fc67-139">В следующем примере hello конечной точкой CDN явно зависит от профиля CDN hello и неявно зависит от веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4fc67-139">In hello following example, a CDN endpoint explicitly depends on hello CDN profile, and implicitly depends on a web app.</span></span>

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

<span data-ttu-id="4fc67-140">Можно использовать этот элемент или hello зависимости toospecify элемент dependsOn, но не требуется для hello toouse оба же зависимый ресурс.</span><span class="sxs-lookup"><span data-stu-id="4fc67-140">You can use either this element or hello dependsOn element toospecify dependencies, but you do not need toouse both for hello same dependent resource.</span></span> <span data-ttu-id="4fc67-141">По возможности используйте tooavoid неявные ссылки, добавление ненужные зависимости.</span><span class="sxs-lookup"><span data-stu-id="4fc67-141">Whenever possible, use an implicit reference tooavoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="4fc67-142">toolearn более, в разделе [ссылки на функцию](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="4fc67-142">toolearn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="4fc67-143">Рекомендации по установке зависимостей</span><span class="sxs-lookup"><span data-stu-id="4fc67-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="4fc67-144">При определении того, какие зависимости tooset, используйте hello, следование правилам:</span><span class="sxs-lookup"><span data-stu-id="4fc67-144">When deciding what dependencies tooset, use hello following guidelines:</span></span>

* <span data-ttu-id="4fc67-145">Устанавливайте как можно меньше зависимостей.</span><span class="sxs-lookup"><span data-stu-id="4fc67-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="4fc67-146">Назначайте дочерний ресурс зависимым от его родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="4fc67-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="4fc67-147">Используйте hello **ссылки** функции tooset неявные зависимости между ресурсами, которые должны tooshare свойство.</span><span class="sxs-lookup"><span data-stu-id="4fc67-147">Use hello **reference** function tooset implicit dependencies between resources that need tooshare a property.</span></span> <span data-ttu-id="4fc67-148">Не добавляйте явную зависимость (**dependsOn**), если уже определена неявная зависимость.</span><span class="sxs-lookup"><span data-stu-id="4fc67-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="4fc67-149">Этот подход уменьшает риск hello ненужные зависимости.</span><span class="sxs-lookup"><span data-stu-id="4fc67-149">This approach reduces hello risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="4fc67-150">Задавайте зависимость, когда ресурс не может быть **создан** без функциональных возможностей другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="4fc67-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="4fc67-151">Не задавайте зависимости ресурсов hello взаимодействовать только после развертывания.</span><span class="sxs-lookup"><span data-stu-id="4fc67-151">Do not set a dependency if hello resources only interact after deployment.</span></span>
* <span data-ttu-id="4fc67-152">Позвольте зависимостям задействоваться последовательно, не задавая их явно.</span><span class="sxs-lookup"><span data-stu-id="4fc67-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="4fc67-153">Например виртуальной машины зависит от виртуального сетевого интерфейса и hello виртуального сетевого интерфейса зависит от виртуальной сети и общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="4fc67-153">For example, your virtual machine depends on a virtual network interface, and hello virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="4fc67-154">Таким образом развернутые ресурсы после того как все три — hello виртуальной машины, но не задано явно hello виртуальной машины как зависимость от всех трех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4fc67-154">Therefore, hello virtual machine is deployed after all three resources, but do not explicitly set hello virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="4fc67-155">Этот подход поясняется порядок зависимостей hello и делает его проще шаблон toochange hello позже.</span><span class="sxs-lookup"><span data-stu-id="4fc67-155">This approach clarifies hello dependency order and makes it easier toochange hello template later.</span></span>
* <span data-ttu-id="4fc67-156">Если значение может быть определено до развертывания, попробуйте выполните развертывание ресурсов hello без зависимостей.</span><span class="sxs-lookup"><span data-stu-id="4fc67-156">If a value can be determined before deployment, try deploying hello resource without a dependency.</span></span> <span data-ttu-id="4fc67-157">Например если значение конфигурации должен hello имя другого ресурса, может не требоваться зависимость.</span><span class="sxs-lookup"><span data-stu-id="4fc67-157">For example, if a configuration value needs hello name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="4fc67-158">В этом руководстве не всегда работает, поскольку некоторые ресурсы проверять существование hello hello другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="4fc67-158">This guidance does not always work because some resources verify hello existence of hello other resource.</span></span> <span data-ttu-id="4fc67-159">Если произошла ошибка, добавьте зависимость.</span><span class="sxs-lookup"><span data-stu-id="4fc67-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="4fc67-160">Resource Manager выявляет циклические зависимости во время проверки шаблона.</span><span class="sxs-lookup"><span data-stu-id="4fc67-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="4fc67-161">Если появится сообщение о том, что существует циклическая зависимость, оценка toosee ваш шаблон, если все зависимости не нужны и может быть удален.</span><span class="sxs-lookup"><span data-stu-id="4fc67-161">If you receive an error stating that a circular dependency exists, evaluate your template toosee if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="4fc67-162">Если удаление зависимостей не работает, можно избежать, переместив некоторые операции развертывания в дочерние ресурсы, которые развертываются после hello ресурсов, имеющих циклическую зависимость hello циклические зависимости.</span><span class="sxs-lookup"><span data-stu-id="4fc67-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after hello resources that have hello circular dependency.</span></span> <span data-ttu-id="4fc67-163">Предположим, например, две виртуальные машины развертываются, но необходимо задать свойства для каждого из них, которые ссылаются другие toohello.</span><span class="sxs-lookup"><span data-stu-id="4fc67-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="4fc67-164">Их можно развернуть в hello следующий порядок:</span><span class="sxs-lookup"><span data-stu-id="4fc67-164">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="4fc67-165">vm1.</span><span class="sxs-lookup"><span data-stu-id="4fc67-165">vm1</span></span>
2. <span data-ttu-id="4fc67-166">vm2.</span><span class="sxs-lookup"><span data-stu-id="4fc67-166">vm2</span></span>
3. <span data-ttu-id="4fc67-167">Расширение на vm1 зависит от vm1 и vm2.</span><span class="sxs-lookup"><span data-stu-id="4fc67-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="4fc67-168">расширение Hello задает значения по vm1, получаемый от vm2.</span><span class="sxs-lookup"><span data-stu-id="4fc67-168">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="4fc67-169">Расширение на vm2 зависит от vm1 и vm2.</span><span class="sxs-lookup"><span data-stu-id="4fc67-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="4fc67-170">расширение Hello задает значения по vm2, получаемый от vm1.</span><span class="sxs-lookup"><span data-stu-id="4fc67-170">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="4fc67-171">Сведения об оценке hello порядок развертывания и устранять ошибки зависимостей в разделе [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4fc67-171">For information about assessing hello deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fc67-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4fc67-172">Next steps</span></span>
* <span data-ttu-id="4fc67-173">toolearn об устранении неполадок зависимости во время развертывания, в разделе [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4fc67-173">toolearn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="4fc67-174">toolearn о создании шаблонов диспетчера ресурсов Azure в разделе [разработки шаблонов](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4fc67-174">toolearn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="4fc67-175">Список доступных функций hello в шаблоне см. в разделе [функции шаблона](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="4fc67-175">For a list of hello available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

