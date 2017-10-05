---
title: "О размерах образов виртуальных машин Linux в Azure | Документация Майкрософт"
description: "Узнайте, как используются образы Linux для виртуальных машин в Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: e6ea8adc-4e7a-467a-9394-cd05e67898b7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/21/2016
ms.author: cynthn
ms.openlocfilehash: 187642db18806f4034dcecf4c25b5c71028fdfe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="about-images-for-linux-virtual-machines"></a><span data-ttu-id="0350a-103">Об образах виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="0350a-103">About images for Linux virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0350a-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0350a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0350a-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="0350a-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0350a-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0350a-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="0350a-107">Дополнительные сведения об образах, использующих модель Resource Manager, см. [здесь](../cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0350a-107">For information about images using the Resource Manager model, see [here](../cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="0350a-108">Работа с образами</span><span class="sxs-lookup"><span data-stu-id="0350a-108">Working with images</span></span>
<span data-ttu-id="0350a-109">Для управления образами, доступными по вашей подписке Azure, вы можете использовать интерфейс командной строки Azure (Azure CLI) для Mac, Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="0350a-109">You can use the Azure Command-Line Interface (CLI) for Mac, Linux, and Windows to manage the images available to your Azure subscription.</span></span> <span data-ttu-id="0350a-110">Вы также можете решить некоторые задачи на портале Azure, однако командная строка предоставляет больше возможностей.</span><span class="sxs-lookup"><span data-stu-id="0350a-110">You also can use the Azure portal for some image tasks, but the command line gives you more options.</span></span>

<span data-ttu-id="0350a-111">Примеры использования этих инструментов приведены в разделе [Основные команды Azure CLI в Linux и Mac](../cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0350a-111">For examples of using the tools, see [Common Azure CLI commands on Linux and Mac](../cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0350a-112">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0350a-112">Next steps</span></span>
<span data-ttu-id="0350a-113">Вы можете [передать собственный образ](create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="0350a-113">You can also [upload your own image](create-upload-vhd.md).</span></span>
