---
title: "aaaDefine дочерний ресурс в шаблоне Azure | Документы Microsoft"
description: "Показано, как tooset hello тип ресурса и имя для дочерних ресурса в шаблоне диспетчера ресурсов Azure"
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
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="2fce0-103">Указание имени и типа дочернего ресурса в шаблоне Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2fce0-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="2fce0-104">При создании шаблона, необходимо часто tooinclude дочерний ресурс, который является связанные tooa родительский ресурс.</span><span class="sxs-lookup"><span data-stu-id="2fce0-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="2fce0-105">Например, шаблон может содержать сервер SQL Server и базу данных.</span><span class="sxs-lookup"><span data-stu-id="2fce0-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="2fce0-106">Hello SQL server hello родительский ресурс, который hello базы данных hello дочерний ресурс.</span><span class="sxs-lookup"><span data-stu-id="2fce0-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="2fce0-107">Hello hello дочерний ресурс типа выглядит следующим образом:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="2fce0-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="2fce0-108">Hello имени ресурса дочерних hello выглядит следующим образом:`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="2fce0-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="2fce0-109">Однако указать hello тип и имя в шаблоне по-разному на основе он вложен в родительский ресурс hello, или сам по себе на верхнем уровне hello.</span><span class="sxs-lookup"><span data-stu-id="2fce0-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="2fce0-110">В этом разделе показано, как подход к toohandle оба.</span><span class="sxs-lookup"><span data-stu-id="2fce0-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="2fce0-111">При создании ресурса tooa полную ссылку, toocombine порядок hello сегменты из типа hello и имя не является просто объединение двух hello.</span><span class="sxs-lookup"><span data-stu-id="2fce0-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="2fce0-112">Вместо этого после приветствия имен, используйте последовательность *тип/имя* пар из определенного в указанном toomost:</span><span class="sxs-lookup"><span data-stu-id="2fce0-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="2fce0-113">Например:</span><span class="sxs-lookup"><span data-stu-id="2fce0-113">For example:</span></span>

<span data-ttu-id="2fce0-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` — правильно, `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` — неправильно.</span><span class="sxs-lookup"><span data-stu-id="2fce0-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="2fce0-115">Вложенный дочерний ресурс</span><span class="sxs-lookup"><span data-stu-id="2fce0-115">Nested child resource</span></span>
<span data-ttu-id="2fce0-116">toodefine простым способом Hello дочерний ресурс является toonest его в родительский ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="2fce0-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="2fce0-117">Hello пример базы данных SQL, вложенных в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fce0-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

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

<span data-ttu-id="2fce0-118">Для hello дочерних ресурса, тип hello установлен слишком`databases` , но его тип ресурсов — `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="2fce0-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="2fce0-119">Не указано `Microsoft.Sql/servers/` так, как предполагалось, из типа ресурса родительского hello.</span><span class="sxs-lookup"><span data-stu-id="2fce0-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="2fce0-120">слишком задано имя ресурса дочерних Hello`exampledatabase` но hello полное имя включает имя родительского hello.</span><span class="sxs-lookup"><span data-stu-id="2fce0-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="2fce0-121">Не указано `exampleserver` так, как предполагалось, из родительского ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="2fce0-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="2fce0-122">Дочерний ресурс верхнего уровня</span><span class="sxs-lookup"><span data-stu-id="2fce0-122">Top-level child resource</span></span>
<span data-ttu-id="2fce0-123">Можно определить hello дочерний ресурс на верхнем уровне hello.</span><span class="sxs-lookup"><span data-stu-id="2fce0-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="2fce0-124">Этот подход можно использовать, если родительский ресурс hello не развернут в hello того же шаблона или, если хотите toouse `copy` toocreate несколько дочерние ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2fce0-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="2fce0-125">При таком подходе необходимо указать тип полного ресурса hello и включить имя родительского ресурса hello в имя ресурса дочернего hello.</span><span class="sxs-lookup"><span data-stu-id="2fce0-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

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

<span data-ttu-id="2fce0-126">Hello базы данных является дочерним сервером toohello ресурсов, даже если они определены в hello же уровня в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="2fce0-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fce0-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2fce0-127">Next steps</span></span>
* <span data-ttu-id="2fce0-128">Рекомендации о том, как toocreate шаблонов, см. раздел [советы и рекомендации по созданию шаблонов диспетчера ресурсов Azure](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="2fce0-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="2fce0-129">Пример создания нескольких дочерних ресурсов см. в разделе [Развертывание нескольких экземпляров ресурсов в шаблонах Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2fce0-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
