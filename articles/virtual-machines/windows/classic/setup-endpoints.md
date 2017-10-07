---
title: "aaaSet копирование конечные точки в классической виртуальной Машине Windows | Документы Microsoft"
description: "Узнайте tooset настройке конечных точек для виртуальной Машины Windows в hello Azure классического портала tooallow связи с виртуальной машины Windows в Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="4d172-103">Как tooset копирование конечные точки в классической виртуальной машине в Azure</span><span class="sxs-lookup"><span data-stu-id="4d172-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="4d172-104">Все виртуальные машины, создаваемые в Azure с помощью hello классической модели развертывания, могут автоматически взаимодействовать через канал частной сети с другими виртуальными машинами в Windows hello одной облачной службе или виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4d172-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="4d172-105">Однако hello Интернет или другими виртуальными сетями компьютеров требуется конечные точки toodirect hello входящего сетевого трафика tooa виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4d172-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="4d172-106">Также доступна версия этой статьи для [виртуальных машин Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="4d172-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d172-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4d172-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4d172-108">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="4d172-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4d172-109">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4d172-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="4d172-110">В hello **диспетчера ресурсов** модель развертывания, настройки конечных точек с помощью **группы безопасности сети (Nsg)**.</span><span class="sxs-lookup"><span data-stu-id="4d172-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="4d172-111">Дополнительные сведения см. в разделе [разрешить внешний доступ tooyour виртуальной Машины с помощью портала Azure "hello"](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d172-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="4d172-112">При создании виртуальной машины Windows в hello портал Azure общие конечные точки, как и для удаленного рабочего стола и удаленного взаимодействия Windows PowerShell обычно создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="4d172-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="4d172-113">При создании виртуальной машины hello, либо уже после этого при необходимости можно настроить дополнительные конечные точки.</span><span class="sxs-lookup"><span data-stu-id="4d172-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="4d172-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d172-114">Next steps</span></span>
* <span data-ttu-id="4d172-115">toouse tooset командлет Azure PowerShell копирование конечной точки виртуальной Машины в разделе [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d172-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="4d172-116">toouse toomanage командлет Azure PowerShell ACL для конечной точки, в разделе [управление списки управления доступом (ACL) для конечных точек с помощью PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4d172-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="4d172-117">При создании виртуальной машины в модели развертывания диспетчера ресурсов hello Azure PowerShell можно использовать слишком[создавать группы безопасности сети](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toohello toocontrol трафик виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4d172-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
