---
title: "Добавление тега к виртуальной машине Linux в Azure | Документация Майкрософт"
description: "Узнайте, как добавлять теги к виртуальной машине Linux, созданной в Azure с использованием модели развертывания с помощью Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: f643001c85e127ae39e9869ffdc689bcac232ccb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="4e569-103">Пометка виртуальной машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="4e569-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="4e569-104">В этой статье описываются разные способы назначения тегов виртуальной машине Linux в Azure с использованием модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4e569-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="4e569-105">Теги — это определяемые пользователем пары "ключ-значение", которые можно помещать непосредственно в ресурс или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4e569-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="4e569-106">В настоящий момент Azure поддерживает до 15 тегов на ресурс или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4e569-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="4e569-107">Теги можно добавлять к ресурсу во время его создания или к уже существующему ресурсу.</span><span class="sxs-lookup"><span data-stu-id="4e569-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="4e569-108">Обратите внимание, что теги поддерживаются только для тех ресурсов, которые созданы с помощью модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4e569-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="4e569-109">Отметка тегами с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="4e569-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="4e569-110">Сначала [установите и настройте интерфейс командной строки Azure](../../xplat-cli-azure-resource-manager.md). При этом обязательно включите режим Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="4e569-110">To begin, [install and configure the Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="4e569-111">Вы можете просмотреть все свойства определенной виртуальной машины, включая теги, с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="4e569-111">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="4e569-112">Чтобы добавить новый тег виртуальной машины через интерфейс командной строки Azure, можно применить команду `azure vm set` с параметром тега **-t**:</span><span class="sxs-lookup"><span data-stu-id="4e569-112">To add a new VM tag through the Azure CLI, you can use the `azure vm set` command along with the tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="4e569-113">Чтобы удалить все теги, используйте в команде `azure vm set` параметр **–T**.</span><span class="sxs-lookup"><span data-stu-id="4e569-113">To remove all tags, you can use the **–T** parameter in the `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="4e569-114">Теперь, когда мы применили теги к ресурсам с помощью Azure CLI и портала, рассмотрим сведения об использовании, чтобы увидеть теги на портале выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="4e569-114">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="4e569-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e569-115">Next steps</span></span>
* <span data-ttu-id="4e569-116">Дополнительные сведения о добавлении тегов для ресурсов Azure см. в статьях [Общие сведения об Azure Resource Manager][Azure Resource Manager Overview] и [Использование тегов для организации ресурсов в Azure][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="4e569-116">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="4e569-117">Сведения о том, как теги могут помочь в управлении использованием ресурсов Azure, см. в статьях [Расшифровка счета за использование Microsoft Azure][Understanding your Azure Bill] и [Получение ценных сведений о потреблении ресурсов Microsoft Azure][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="4e569-117">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
