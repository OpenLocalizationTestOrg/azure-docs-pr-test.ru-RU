---
title: "размеры виртуальных Машин Linux aaaAzure - GPU | Документы Microsoft"
description: "Список hello разных GPU оптимизированными размеры, доступные для виртуальных машин Linux в Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="9d4a8-103">Размеры виртуальных машин Linux, оптимизированных для GPU</span><span class="sxs-lookup"><span data-stu-id="9d4a8-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="9d4a8-104">Инструкции по установке и проверке драйверов см. в статье [Установка драйверов GPU NVIDIA на виртуальные машины серии N под управлением Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9d4a8-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="9d4a8-105">Не рекомендуется устанавливать X server или другими системами, использующие драйвер nouveau hello на виртуальных машинах Ubuntu NC.</span><span class="sxs-lookup"><span data-stu-id="9d4a8-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="9d4a8-106">Перед установкой драйверов GPU, NVIDIA, необходим драйвер nouveau toodisable hello.</span><span class="sxs-lookup"><span data-stu-id="9d4a8-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="9d4a8-107">Остальные размеры</span><span class="sxs-lookup"><span data-stu-id="9d4a8-107">Other sizes</span></span>
- [<span data-ttu-id="9d4a8-108">Универсальные</span><span class="sxs-lookup"><span data-stu-id="9d4a8-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="9d4a8-109">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="9d4a8-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="9d4a8-110">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="9d4a8-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="9d4a8-111">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="9d4a8-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="9d4a8-112">Для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="9d4a8-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="9d4a8-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9d4a8-113">Next steps</span></span>
<span data-ttu-id="9d4a8-114">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="9d4a8-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>