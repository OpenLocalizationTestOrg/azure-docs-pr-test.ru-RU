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
ms.openlocfilehash: da3ff0de2a5d6ac8994b7c16b758f976228a53b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="ae452-103">Пометка виртуальной машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="ae452-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="ae452-104">В этой статье описываются разные способы назначения тегов виртуальной машине Linux в Azure с использованием модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ae452-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="ae452-105">Теги — это определяемые пользователем пары "ключ-значение", которые можно помещать непосредственно в ресурс или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ae452-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="ae452-106">В настоящий момент Azure поддерживает до 15 тегов на ресурс или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ae452-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="ae452-107">Теги можно добавлять к ресурсу во время его создания или к уже существующему ресурсу.</span><span class="sxs-lookup"><span data-stu-id="ae452-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="ae452-108">Обратите внимание, что теги поддерживаются только для тех ресурсов, которые созданы с помощью модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ae452-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="ae452-109">Отметка тегами с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="ae452-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="ae452-110">Чтобы начать работу, вам нужно установить последнюю версию [Azure CLI 2.0 (предварительная версия)](/cli/azure/install-az-cli2) и войти в учетную запись Azure, выполнив команду [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ae452-110">To begin, you need the latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="ae452-111">Эти действия можно также выполнить с помощью [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae452-111">You can also perform these steps with the [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ae452-112">Вы можете просмотреть все свойства определенной виртуальной машины, включая теги, с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="ae452-112">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="ae452-113">Чтобы добавить новый тег виртуальной машины через Azure CLI, можно применить команду `azure vm update` с параметром тега **--set**:</span><span class="sxs-lookup"><span data-stu-id="ae452-113">To add a new VM tag through the Azure CLI, you can use the `azure vm update` command along with the tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="ae452-114">Чтобы удалить теги, используйте в команде `azure vm update` параметр **--remove**.</span><span class="sxs-lookup"><span data-stu-id="ae452-114">To remove tags, you can use the **--remove** parameter in the `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="ae452-115">Теперь, когда мы применили теги к ресурсам с помощью Azure CLI и портала, рассмотрим сведения об использовании, чтобы увидеть теги на портале выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="ae452-115">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="ae452-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ae452-116">Next steps</span></span>
* <span data-ttu-id="ae452-117">Дополнительные сведения о добавлении тегов для ресурсов Azure см. в статьях [Общие сведения об Azure Resource Manager][Azure Resource Manager Overview] и [Использование тегов для организации ресурсов в Azure][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="ae452-117">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="ae452-118">Сведения о том, как теги могут помочь в управлении использованием ресурсов Azure, см. в статьях [Расшифровка счета за использование Microsoft Azure][Understanding your Azure Bill] и [Получение ценных сведений о потреблении ресурсов Microsoft Azure][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="ae452-118">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
