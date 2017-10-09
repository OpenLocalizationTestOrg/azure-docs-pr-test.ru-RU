---
title: "aaaHow tootag виртуальной машине Azure Linux | Документы Microsoft"
description: "Дополнительные сведения о виртуальной машине Azure Linux, созданные в Azure с помощью модели развертывания диспетчера ресурсов hello тегов."
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
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="df973-103">Как tootag виртуальной машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="df973-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="df973-104">Этой статье описываются различные способы tootag виртуальной машины Linux в Azure через hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="df973-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="df973-105">Теги — это определяемые пользователем пары "ключ-значение", которые можно помещать непосредственно в ресурс или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="df973-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="df973-106">В настоящее время Azure поддерживает теги too15 каждого ресурса и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="df973-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="df973-107">Теги можно поместить в ресурс во время создания hello или добавлены tooan существующий ресурс.</span><span class="sxs-lookup"><span data-stu-id="df973-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="df973-108">Обратите внимание, теги поддерживаются для ресурсов, созданные с помощью модели развертывания диспетчера ресурсов hello только.</span><span class="sxs-lookup"><span data-stu-id="df973-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="df973-109">Отметка тегами с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="df973-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="df973-110">toobegin, требуется hello последней [Azure CLI 2.0 (Предварительная версия)](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="df973-110">toobegin, you need hello latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="df973-111">Можно также выполнить следующие действия с hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="df973-111">You can also perform these steps with hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="df973-112">Можно просмотреть все свойства для данной виртуальной машине, в том числе теги hello, с помощью этой команды:</span><span class="sxs-lookup"><span data-stu-id="df973-112">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="df973-113">tooadd новый тег виртуальной Машины через hello Azure CLI можно использовать hello `azure vm update` команды и параметра тег hello **--задать**:</span><span class="sxs-lookup"><span data-stu-id="df973-113">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm update` command along with hello tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="df973-114">теги tooremove можно использовать hello **--удаление** параметр в hello `azure vm update` команды.</span><span class="sxs-lookup"><span data-stu-id="df973-114">tooremove tags, you can use hello **--remove** parameter in hello `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="df973-115">Теперь, когда мы применили теги tooour ресурсы Azure CLI и hello портала, давайте рассмотрим toosee сведения об использовании hello hello теги в портале выставления счетов hello.</span><span class="sxs-lookup"><span data-stu-id="df973-115">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="df973-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df973-116">Next steps</span></span>
* <span data-ttu-id="df973-117">toolearn Дополнительные сведения о тегов ресурсам Azure в разделе [Обзор диспетчера ресурсов Azure] [ Azure Resource Manager Overview] и [tooorganize с помощью тегов ресурсов Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="df973-117">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="df973-118">toosee теги помогают управлять использование ресурсов Azure разделе [основные сведения о счете Azure] [ Understanding your Azure Bill] и [анализировать потребления ресурсов Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="df973-118">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
