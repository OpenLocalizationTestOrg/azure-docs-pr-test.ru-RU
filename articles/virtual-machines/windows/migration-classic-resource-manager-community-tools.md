---
title: "средства aaaCommunity — перемещение tooAzure классические ресурсы диспетчера ресурсов | Документы Microsoft"
description: "Эти средства hello каталоги статьи, предоставляемые hello сообщества toohelp миграции ресурсов IaaS с toohello классической модели развертывания диспетчера ресурсов Azure."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a><span data-ttu-id="510e0-103">Ресурсы IaaS toomigrate из tooAzure классического Resource Manager tools сообщества</span><span class="sxs-lookup"><span data-stu-id="510e0-103">Community tools toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>
<span data-ttu-id="510e0-104">Это статье каталоги hello средства, которые были дополнены по tooassist сообщества hello миграции IaaS ресурсов от toohello классической модели развертывания диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="510e0-104">This article catalogs hello tools that have been provided by hello community tooassist with migration of IaaS resources from classic toohello Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="510e0-105">Эти инструменты официально не поддерживаются службой поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="510e0-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="510e0-106">Таким образом они открыты исходный код на GitHub, и мы довольны tooaccept PR для исправления или дополнительных сценариев.</span><span class="sxs-lookup"><span data-stu-id="510e0-106">Therefore they are open sourced on GitHub and we're happy tooaccept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="510e0-107">tooreport проблему, используйте GitHub проблемы функции hello.</span><span class="sxs-lookup"><span data-stu-id="510e0-107">tooreport an issue, use hello GitHub issues feature.</span></span>
> 
> <span data-ttu-id="510e0-108">Перенос с использованием этих инструментов вызовет простой классической виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="510e0-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="510e0-109">Если вы хотите выполнить поддерживаемый платформой перенос, см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="510e0-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="510e0-110">Поддерживаемые платформой миграции IaaS ресурсов из классической tooAzure диспетчера ресурсов стека</span><span class="sxs-lookup"><span data-stu-id="510e0-110">Platform supported migration of IaaS resources from Classic tooAzure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="510e0-111">Технические близкое знакомство с платформой поддерживается миграция из tooAzure классический диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="510e0-111">Technical Deep Dive on Platform supported migration from Classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="510e0-112">Перенос ресурсов IaaS из классической tooAzure диспетчера ресурсов с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="510e0-112">Migrate IaaS resources from Classic tooAzure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="510e0-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="510e0-113">AsmMetadataParser</span></span>
<span data-ttu-id="510e0-114">Это набор средств поддержки создана как часть enterprise для миграции из tooAzure управления службами Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="510e0-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management tooAzure Resource Manager.</span></span> <span data-ttu-id="510e0-115">Это средство позволяет tooreplicate инфраструктуры в другую подписку, который может использоваться для проверки миграции и положите проблемы, перед выполнением миграции hello на вашей производственной подписке.</span><span class="sxs-lookup"><span data-stu-id="510e0-115">This tool allows you tooreplicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running hello migration on your Production subscription.</span></span>

[<span data-ttu-id="510e0-116">Документацию к инструменту toohello ссылку</span><span class="sxs-lookup"><span data-stu-id="510e0-116">Link toohello tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="510e0-117">migAz</span><span class="sxs-lookup"><span data-stu-id="510e0-117">migAz</span></span>
<span data-ttu-id="510e0-118">migAz является дополнительным параметром toomigrate полный набор классические ресурсы IaaS диспетчера ресурсов tooAzure ресурсов IaaS.</span><span class="sxs-lookup"><span data-stu-id="510e0-118">migAz is an additional option toomigrate a complete set of classic IaaS resources tooAzure Resource Manager IaaS resources.</span></span> <span data-ttu-id="510e0-119">Hello миграции могут встречаться в hello же подписки или между разными подписками и типы подписок (ex: подписок CSP).</span><span class="sxs-lookup"><span data-stu-id="510e0-119">hello migration can occur within hello same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="510e0-120">Документацию к инструменту toohello ссылку</span><span class="sxs-lookup"><span data-stu-id="510e0-120">Link toohello tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="510e0-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="510e0-121">Next Steps</span></span>

* [<span data-ttu-id="510e0-122">Общие сведения о миграции поддерживаются платформы IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="510e0-122">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="510e0-123">Технические близкое знакомство с платформа поддерживается перенос из классической tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="510e0-123">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="510e0-124">Планирование миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="510e0-124">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="510e0-125">Использовать ресурсы IaaS PowerShell toomigrate из классической tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="510e0-125">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="510e0-126">Использовать ресурсы IaaS toomigrate CLI из классической tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="510e0-126">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="510e0-127">Распространенные ошибки миграции</span><span class="sxs-lookup"><span data-stu-id="510e0-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="510e0-128">Просмотрите hello наиболее часто задаваемые вопросы о миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="510e0-128">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

