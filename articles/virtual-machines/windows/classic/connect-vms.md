---
title: "Подключение виртуальных машин Windows в облачной службе | Документация Майкрософт"
description: "Подключение виртуальных машин Windows, созданных с помощью классической модели развертывания, к облачной службе Azure или виртуальной сети."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c1cbc802-4352-4d2e-9e49-4ccbd955324b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: 0c7a21461e5bb111c4359df8e949d48382b591c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-virtual-machines-created-with-the-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="ee9be-103">Подключение виртуальных машин Windows, созданных с помощью классической модели развертывания, к виртуальной сети или облачной службе</span><span class="sxs-lookup"><span data-stu-id="ee9be-103">Connect Windows virtual machines created with the classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ee9be-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ee9be-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ee9be-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ee9be-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ee9be-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ee9be-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="ee9be-107">Виртуальные машины Windows, созданные по классической модели развертывания, всегда размещаются в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="ee9be-107">Windows virtual machines created with the classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="ee9be-108">Облачная служба выступает в качестве контейнера и предоставляет уникальное общедоступное DNS-имя, общедоступный IP-адрес и набор конечных точек для доступа к виртуальной машине через Интернет.</span><span class="sxs-lookup"><span data-stu-id="ee9be-108">The cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints to access the virtual machine over the Internet.</span></span> <span data-ttu-id="ee9be-109">Облачная служба может находиться в виртуальной сети, но это не обязательно.</span><span class="sxs-lookup"><span data-stu-id="ee9be-109">The cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="ee9be-110">Вы также можете [подключить виртуальные машины Linux к виртуальной сети или облачной службе](../../linux/classic/connect-vms.md).</span><span class="sxs-lookup"><span data-stu-id="ee9be-110">You can also [connect Linux virtual machines with a virtual network or cloud service](../../linux/classic/connect-vms.md).</span></span>

<span data-ttu-id="ee9be-111">Если облачная служба не находится в виртуальной сети, она называется *автономной* .</span><span class="sxs-lookup"><span data-stu-id="ee9be-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="ee9be-112">Виртуальные машины в изолированной облачной службе могут взаимодействовать с другими виртуальными машинами с помощью их общедоступных DNS-имен, при этом трафик проходит через Интернет.</span><span class="sxs-lookup"><span data-stu-id="ee9be-112">The virtual machines in a standalone cloud service communicate with other virtual machines by using the other virtual machines’ public DNS names, and the traffic travels over the Internet.</span></span> <span data-ttu-id="ee9be-113">Если облачная служба находится в виртуальной сети, виртуальные машины в этой облачной службе могут взаимодействовать со всеми остальными виртуальными машинами в виртуальной сети без отправки трафика через Интернет.</span><span class="sxs-lookup"><span data-stu-id="ee9be-113">If a cloud service is in a virtual network, the virtual machines in that cloud service can communicate with all other virtual machines in the virtual network without sending any traffic over the Internet.</span></span>

<span data-ttu-id="ee9be-114">Если разместить виртуальные машины в одной автономной облачной службе, можно использовать балансировку нагрузки и группы доступности.</span><span class="sxs-lookup"><span data-stu-id="ee9be-114">If you place your virtual machines in the same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="ee9be-115">Дополнительные сведения см. в разделах [Балансировка нагрузки виртуальных машин](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и [Управление доступностью виртуальных машин](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ee9be-115">For details, see [Load balancing virtual machines](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Manage the availability of virtual machines](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ee9be-116">Тем не менее, невозможно упорядочить виртуальные машины в подсетях или подключить автономную облачную службу к локальной сети.</span><span class="sxs-lookup"><span data-stu-id="ee9be-116">However, you can't organize the virtual machines on subnets or connect a standalone cloud service to your on-premises network.</span></span> <span data-ttu-id="ee9be-117">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="ee9be-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="ee9be-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee9be-118">Next steps</span></span>
<span data-ttu-id="ee9be-119">После создания виртуальной машины рекомендуется [добавить диск данных](attach-disk.md) , чтобы ваши службы и рабочие нагрузки имели расположение для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="ee9be-119">After you create a virtual machine, it's a good idea to [add a data disk](attach-disk.md) so your services and workloads have a location to store data.</span></span>
