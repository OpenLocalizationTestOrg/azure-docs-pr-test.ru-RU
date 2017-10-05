---
title: "Связанные ресурсы в коллекции плиток"
description: "Дополнительные сведения о связанных ресурсах, отображаемых в коллекции плиток на портале предварительной версии Azure."
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: efa7bce26c2c4c153b083e0e34d689a11d27dd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="related-and-linked-resources-in-the-tile-gallery"></a><span data-ttu-id="151e1-103">Связанные ресурсы в коллекции плиток</span><span class="sxs-lookup"><span data-stu-id="151e1-103">Related and linked resources in the tile gallery</span></span>
<span data-ttu-id="151e1-104">В коллекции плиток вы можете найти плитки для конкретного ресурса, чтобы перетащить их в свою текущую колонку.</span><span class="sxs-lookup"><span data-stu-id="151e1-104">The tile gallery enables you to find tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="151e1-105">Используя коллекцию плиток, вы можете создавать представления управления, связывающие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="151e1-105">Using the tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="151e1-106">Ресурсы, связанные с выбранным ресурсом, включают все ресурсы в группе ресурсов, а также все ресурсы, которые ссылаются на этот ресурс или на которые ссылается ресурс.</span><span class="sxs-lookup"><span data-stu-id="151e1-106">For any specified resource, the related resources include all the resources in its resource group, and any resources that link to or from the resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="151e1-107">Связанные ресурсы в Resource Manager</span><span class="sxs-lookup"><span data-stu-id="151e1-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="151e1-108">Связывание — это функция Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="151e1-108">Linking is a feature of the Resource Manager.</span></span>  <span data-ttu-id="151e1-109">Она позволяет объявлять отношения между ресурсами, даже если они не находятся в одной и той же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="151e1-109">It enables you to declare relationships between resources even if they do not reside in the same resource group.</span></span> <span data-ttu-id="151e1-110">Связывание не влияет на среду выполнения ресурсов, выставление счетов или доступ на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="151e1-110">Linking has no impact on the runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="151e1-111">Это просто механизм, который можно использовать для представления связей, чтобы такие средства, как коллекция плиток, могли предоставлять широкие возможности управления.</span><span class="sxs-lookup"><span data-stu-id="151e1-111">It's simply a mechanism you can use to represent relationships so that tools like the tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="151e1-112">Ваши средства могут проверять ссылки, используя API ссылок. Кроме того, они могут предоставлять настраиваемые возможности управления отношениями.</span><span class="sxs-lookup"><span data-stu-id="151e1-112">Your tools can inspect the links using the links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="151e1-113">Как связать ресурсы?</span><span class="sxs-lookup"><span data-stu-id="151e1-113">How do I link my resources?</span></span>
<span data-ttu-id="151e1-114">Во время создания ресурсов на портале либо путем развертывания шаблона с использованием Azure PowerShell или Azure CLI для некоторых зависимых ресурсов ссылки создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="151e1-114">When you create resources through the portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="151e1-115">Вы также можете программно связать ресурсы с помощью [REST API связанных ресурсов](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="151e1-115">You can also programmatically link resources by using the [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="151e1-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="151e1-116">Next steps</span></span>
* <span data-ttu-id="151e1-117">Если вам нужна информация для написания шаблонов Resource Manager, то см. статью [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="151e1-117">If you need an introduction to writing Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="151e1-118">Чтобы узнать больше о работе с группами ресурсов на портале, см. статью [Управление ресурсами Azure через портал](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="151e1-118">To understand more about working with resource groups through the portal, see [Using the Azure portal to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

