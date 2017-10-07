---
title: "aaaRelated и связанные ресурсы в hello плитку коллекции"
description: "Дополнительные сведения о связанных и связанными ресурсами, отображаемых в галерее плитки приветствия hello Azure предварительной версии портала."
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
ms.openlocfilehash: c8f99be8e23dc9641ec3cd3169604b33a4b049f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="related-and-linked-resources-in-hello-tile-gallery"></a><span data-ttu-id="298d7-103">Связанные и связанными ресурсами в галерее плитки приветствия</span><span class="sxs-lookup"><span data-stu-id="298d7-103">Related and linked resources in hello tile gallery</span></span>
<span data-ttu-id="298d7-104">Коллекция плитки приветствия позволяет toofind плитки для определенного ресурса и перетащите их на вашей текущей колонки.</span><span class="sxs-lookup"><span data-stu-id="298d7-104">hello tile gallery enables you toofind tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="298d7-105">С помощью коллекции плитки приветствия, можно создать административные представления, занимающих ресурсы.</span><span class="sxs-lookup"><span data-stu-id="298d7-105">Using hello tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="298d7-106">Для любого указанного ресурса hello связанные ресурсы включают все ресурсы hello в ее группа ресурсов и все ресурсы, которые связать tooor из ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="298d7-106">For any specified resource, hello related resources include all hello resources in its resource group, and any resources that link tooor from hello resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="298d7-107">Связанные ресурсы в Resource Manager</span><span class="sxs-lookup"><span data-stu-id="298d7-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="298d7-108">Связывание — это функция hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="298d7-108">Linking is a feature of hello Resource Manager.</span></span>  <span data-ttu-id="298d7-109">Благодаря этому можно toodeclare отношений между ресурсами даже если они находятся в различных hello же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="298d7-109">It enables you toodeclare relationships between resources even if they do not reside in hello same resource group.</span></span> <span data-ttu-id="298d7-110">Связывание не оказывает влияния на время выполнения hello ресурсов, без влияния на выставление счетов и без влияния на доступ на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="298d7-110">Linking has no impact on hello runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="298d7-111">Это просто механизм связи toorepresent можно использовать, чтобы при возникновении таких средств как коллекции hello плитки можно предоставить широкие возможности управления.</span><span class="sxs-lookup"><span data-stu-id="298d7-111">It's simply a mechanism you can use toorepresent relationships so that tools like hello tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="298d7-112">Средства могут проверять hello ссылки с помощью связей hello API и предоставляют пользовательские связи выполнения задач по управлению также.</span><span class="sxs-lookup"><span data-stu-id="298d7-112">Your tools can inspect hello links using hello links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="298d7-113">Как связать ресурсы?</span><span class="sxs-lookup"><span data-stu-id="298d7-113">How do I link my resources?</span></span>
<span data-ttu-id="298d7-114">При создании ресурсов через портал hello или путем развертывания шаблона с помощью Azure PowerShell или Azure CLI, связи создаются автоматически для некоторых зависимых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="298d7-114">When you create resources through hello portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="298d7-115">Вы можете привязать ресурсы также программно с помощью hello [связанные ресурсы REST API](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="298d7-115">You can also programmatically link resources by using hello [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="298d7-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="298d7-116">Next steps</span></span>
* <span data-ttu-id="298d7-117">Найти шаблоны диспетчера ресурсов toowriting введение в разделе [разработки шаблонов](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="298d7-117">If you need an introduction toowriting Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="298d7-118">toounderstand Дополнительные сведения о работе с группами ресурсов через портал hello. в разделе [использование hello Azure портала toomanage ресурсам Azure](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="298d7-118">toounderstand more about working with resource groups through hello portal, see [Using hello Azure portal toomanage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

