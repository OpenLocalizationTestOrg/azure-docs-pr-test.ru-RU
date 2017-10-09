---
title: "aaaAbout, образы виртуальных Машин Linux в Azure | Документы Microsoft"
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
ms.openlocfilehash: f03078cd4c2700782b74452324c964357288b7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-linux-virtual-machines"></a><span data-ttu-id="c6c48-103">Об образах виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="c6c48-103">About images for Linux virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c6c48-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c6c48-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c6c48-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="c6c48-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c6c48-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c6c48-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="c6c48-107">Сведения об изображениях, с помощью диспетчера ресурсов модели hello. в разделе [здесь](../cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6c48-107">For information about images using hello Resource Manager model, see [here](../cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="c6c48-108">Работа с образами</span><span class="sxs-lookup"><span data-stu-id="c6c48-108">Working with images</span></span>
<span data-ttu-id="c6c48-109">Hello Azure интерфейс командной строки (CLI) можно использовать для Mac, Linux и Windows toomanage hello изображения доступен tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c48-109">You can use hello Azure Command-Line Interface (CLI) for Mac, Linux, and Windows toomanage hello images available tooyour Azure subscription.</span></span> <span data-ttu-id="c6c48-110">Hello портал Azure можно использовать для выполнения некоторых задач изображения, но hello командной строки предоставляет дополнительные возможности.</span><span class="sxs-lookup"><span data-stu-id="c6c48-110">You also can use hello Azure portal for some image tasks, but hello command line gives you more options.</span></span>

<span data-ttu-id="c6c48-111">Примеры использования средства hello см. в разделе [Common Azure CLI команды на Mac и Linux](../cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6c48-111">For examples of using hello tools, see [Common Azure CLI commands on Linux and Mac](../cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6c48-112">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6c48-112">Next steps</span></span>
<span data-ttu-id="c6c48-113">Вы можете [передать собственный образ](create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="c6c48-113">You can also [upload your own image](create-upload-vhd.md).</span></span>
