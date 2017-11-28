---
title: "aaaCreate полное доменное имя для виртуальной Машины Windows в hello портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate полное доменное имя или полное доменное имя, для диспетчера ресурсов на основе виртуальной машины в hello портал Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a><span data-ttu-id="7d68b-103">Создание полного доменного имени в hello портал Azure для виртуальной Машины Windows.</span><span class="sxs-lookup"><span data-stu-id="7d68b-103">Create a fully qualified domain name in hello Azure portal for a Windows VM</span></span>

<span data-ttu-id="7d68b-104">При создании виртуальной машины (VM) в hello [портал Azure](https://portal.azure.com), открытому ресурсу IP для hello виртуальной машины создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="7d68b-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="7d68b-105">Можно использовать этот IP адрес tooremotely доступа hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7d68b-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="7d68b-106">Несмотря на то, что портал hello не приводит к созданию [полного доменного имени](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), или полное доменное имя, его можно создать после hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7d68b-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once hello VM is created.</span></span> <span data-ttu-id="7d68b-107">В этой статье демонстрируется toocreate hello действия DNS-имя или полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="7d68b-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="7d68b-108">Создание полного доменного имени</span><span class="sxs-lookup"><span data-stu-id="7d68b-108">Create a FQDN</span></span>
<span data-ttu-id="7d68b-109">Для работы с руководством требуется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="7d68b-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="7d68b-110">При необходимости вы можете [создания виртуальной Машины на портале hello](quick-create-portal.md) или [с помощью Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7d68b-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="7d68b-111">Когда виртуальная машина будет готова, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7d68b-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="7d68b-112">Теперь можно удаленно подключиться toohello виртуальную Машину с помощью этого DNS-имя как для протокола удаленного рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="7d68b-112">You can now connect remotely toohello VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d68b-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7d68b-113">Next steps</span></span>
<span data-ttu-id="7d68b-114">Теперь, когда у виртуальной машины имеется общедоступный IP-адрес и DNS-имя, можно развернуть общие программные платформы или службы, такие как IIS, SQL или SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d68b-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="7d68b-115">Изучите дополнительные сведения об [использовании Resource Manager](../../azure-resource-manager/resource-group-overview.md), чтобы получить советы по созданию развертываний Azure.</span><span class="sxs-lookup"><span data-stu-id="7d68b-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

