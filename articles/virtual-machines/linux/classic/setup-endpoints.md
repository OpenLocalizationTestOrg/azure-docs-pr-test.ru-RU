---
title: "aaaSet копирование конечные точки в классической виртуальной Машины Linux | Документы Microsoft"
description: "Узнайте tooset настройке конечных точек для виртуальной Машины Linux в hello Azure классического портала tooallow связи с виртуальной машины Linux в Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="741d0-103">Как tooset копирование конечные точки в классической виртуальной машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="741d0-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="741d0-104">Все виртуальные машины Linux, созданных в Azure с помощью hello классической модели развертывания могут автоматически взаимодействовать через канал частной сети с другими виртуальными машинами в hello, же облака службы или виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="741d0-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="741d0-105">Однако hello Интернет или другими виртуальными сетями компьютеров требуется конечные точки toodirect hello входящего сетевого трафика tooa виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="741d0-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="741d0-106">Также доступна версия этой статьи для [виртуальных машин Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="741d0-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="741d0-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="741d0-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="741d0-108">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="741d0-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="741d0-109">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="741d0-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="741d0-110">В hello **диспетчера ресурсов** модель развертывания, настройки конечных точек с помощью **группы безопасности сети (Nsg)**.</span><span class="sxs-lookup"><span data-stu-id="741d0-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="741d0-111">Дополнительные сведения см. в статье [Открытие портов и конечных точек](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="741d0-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="741d0-112">При создании виртуальной машины Linux в hello портал Azure конечной точки для Secure Shell (SSH) обычно создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="741d0-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="741d0-113">При создании виртуальной машины hello, либо уже после этого при необходимости можно настроить дополнительные конечные точки.</span><span class="sxs-lookup"><span data-stu-id="741d0-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="741d0-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="741d0-114">Next steps</span></span>
* <span data-ttu-id="741d0-115">Можно также создать конечную точку виртуальной Машины с помощью hello [интерфейса командной строки Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="741d0-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="741d0-116">Запустите hello **конечную точку виртуальной машины Windows azure, создайте** команды.</span><span class="sxs-lookup"><span data-stu-id="741d0-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="741d0-117">При создании виртуальной машины в модели развертывания диспетчера ресурсов hello hello Azure CLI в режим диспетчера ресурсов можно использовать слишком[создавать группы безопасности сети](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toohello toocontrol трафик виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="741d0-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
