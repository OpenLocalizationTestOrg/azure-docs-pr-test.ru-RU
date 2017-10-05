---
title: "Определение дочернего ресурса в шаблоне Azure | Документация Майкрософт"
description: "В этой статье показано, как задать тип и имя дочернего ресурса в шаблоне Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: 5b6ce5526f354008eb4a697deec737876f22391f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="05b77-103">Указание имени и типа дочернего ресурса в шаблоне Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05b77-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="05b77-104">При создании шаблона нередко требуется добавить в него дочерний ресурс, связанный с родительским ресурсом.</span><span class="sxs-lookup"><span data-stu-id="05b77-104">When creating a template, you frequently need to include a child resource that is related to a parent resource.</span></span> <span data-ttu-id="05b77-105">Например, шаблон может содержать сервер SQL Server и базу данных.</span><span class="sxs-lookup"><span data-stu-id="05b77-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="05b77-106">Сервер SQL Server является родительским ресурсом, а база данных — дочерним.</span><span class="sxs-lookup"><span data-stu-id="05b77-106">The SQL server is the parent resource, and the database is the child resource.</span></span> 

<span data-ttu-id="05b77-107">Формат типа дочернего ресурса: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="05b77-107">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="05b77-108">Формат имени дочернего ресурса: `{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="05b77-108">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="05b77-109">Тип и имя указываются в шаблоне по-разному в зависимости от того, является ли дочерний ресурс вложенным в родительский ресурс или самостоятельным ресурсом на верхнем уровне.</span><span class="sxs-lookup"><span data-stu-id="05b77-109">However, you specify the type and name in a template differently based on whether it is nested within the parent resource, or on its own at the top level.</span></span> <span data-ttu-id="05b77-110">В этой статье описываются оба варианта.</span><span class="sxs-lookup"><span data-stu-id="05b77-110">This topic shows how to handle both approaches.</span></span>

<span data-ttu-id="05b77-111">При создании полной ссылки на ресурс порядок объединения сегментов из типа и имени представляет собой не только использование этих двух вариантов.</span><span class="sxs-lookup"><span data-stu-id="05b77-111">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name  is not simply a concatenation of the two.</span></span>  <span data-ttu-id="05b77-112">Вместо этого после пространства имен используйте пары *типа и имени*, начиная от наименее подходящей к наиболее подходящей.</span><span class="sxs-lookup"><span data-stu-id="05b77-112">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="05b77-113">Например:</span><span class="sxs-lookup"><span data-stu-id="05b77-113">For example:</span></span>

<span data-ttu-id="05b77-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` — правильно, `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` — неправильно.</span><span class="sxs-lookup"><span data-stu-id="05b77-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="05b77-115">Вложенный дочерний ресурс</span><span class="sxs-lookup"><span data-stu-id="05b77-115">Nested child resource</span></span>
<span data-ttu-id="05b77-116">Самый простой способ определить дочерний ресурс — вложить его в родительский ресурс.</span><span class="sxs-lookup"><span data-stu-id="05b77-116">The easiest way to define a child resource is to nest it within the parent resource.</span></span> <span data-ttu-id="05b77-117">В следующем примере показана база данных SQL, вложенная в сервер SQL Server.</span><span class="sxs-lookup"><span data-stu-id="05b77-117">The following example shows a SQL database nested within in a SQL Server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="05b77-118">Для дочернего ресурса задается тип `databases`, но его полным типом ресурса является `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="05b77-118">For the child resource, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="05b77-119">`Microsoft.Sql/servers/` не указывается, так как предполагается из типа родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="05b77-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from the parent resource type.</span></span> <span data-ttu-id="05b77-120">Дочернему ресурсу присваивается имя `exampledatabase`, но его полное имя включает в себя имя родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="05b77-120">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span></span> <span data-ttu-id="05b77-121">`exampleserver` не указывается, так как предполагается из родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="05b77-121">You do not provide `exampleserver` because it is assumed from the parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="05b77-122">Дочерний ресурс верхнего уровня</span><span class="sxs-lookup"><span data-stu-id="05b77-122">Top-level child resource</span></span>
<span data-ttu-id="05b77-123">Дочерний ресурс можно определить на верхнем уровне.</span><span class="sxs-lookup"><span data-stu-id="05b77-123">You can define the child resource at the top level.</span></span> <span data-ttu-id="05b77-124">Этот подход можно использовать, если родительский ресурс не развертывается в том же шаблоне или требуется использовать `copy` для создания нескольких дочерних ресурсов.</span><span class="sxs-lookup"><span data-stu-id="05b77-124">You might use this approach if the parent resource is not deployed in the same template, or if want to use `copy` to create multiple child resources.</span></span> <span data-ttu-id="05b77-125">В этом случае нужно указать полный тип ресурса и добавить в имя дочернего ресурса имя родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="05b77-125">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="05b77-126">База данных является дочерним ресурсом для сервера, даже если они определены на одном уровне в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="05b77-126">The database is a child resource to the server even though they are defined on the same level in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05b77-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05b77-127">Next steps</span></span>
* <span data-ttu-id="05b77-128">См. дополнительные рекомендации по [созданию шаблонов Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="05b77-128">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="05b77-129">Пример создания нескольких дочерних ресурсов см. в разделе [Развертывание нескольких экземпляров ресурсов в шаблонах Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="05b77-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
