---
title: "Создание FQDN для виртуальной машины Windows на портале Azure | Документация Майкрософт"
description: "Узнайте, как создать полное доменное имя (FQDN) для виртуальной машины на основе Resource Manager на портале Azure."
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
ms.openlocfilehash: 2d5a555cd873222efcdb29e8eb3aaf128a24414b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-windows-vm"></a><span data-ttu-id="5f03a-103">Создание полного доменного имени на портале Azure для виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="5f03a-103">Create a fully qualified domain name in the Azure portal for a Windows VM</span></span>

<span data-ttu-id="5f03a-104">При создании виртуальной машины на [портале Azure](https://portal.azure.com) для нее автоматически создается ресурс общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="5f03a-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="5f03a-105">Этот IP-адрес используется для удаленного доступа к данной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="5f03a-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="5f03a-106">Несмотря на то что портал не создает [полное доменное имя](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), его можно создать после создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5f03a-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once the VM is created.</span></span> <span data-ttu-id="5f03a-107">В этой статье показан процесс создания DNS-имени или полного доменного имени.</span><span class="sxs-lookup"><span data-stu-id="5f03a-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="5f03a-108">Создание полного доменного имени</span><span class="sxs-lookup"><span data-stu-id="5f03a-108">Create a FQDN</span></span>
<span data-ttu-id="5f03a-109">Для работы с руководством требуется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="5f03a-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="5f03a-110">При необходимости ее можно создать [на портале](quick-create-portal.md) или с помощью [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5f03a-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="5f03a-111">Когда виртуальная машина будет готова, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5f03a-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="5f03a-112">Теперь вы можете удаленно подключиться к виртуальной машине с помощью DNS-имени, например, используя протокол удаленного рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="5f03a-112">You can now connect remotely to the VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f03a-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f03a-113">Next steps</span></span>
<span data-ttu-id="5f03a-114">Теперь, когда у виртуальной машины имеется общедоступный IP-адрес и DNS-имя, можно развернуть общие программные платформы или службы, такие как IIS, SQL или SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f03a-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="5f03a-115">Изучите дополнительные сведения об [использовании Resource Manager](../../azure-resource-manager/resource-group-overview.md), чтобы получить советы по созданию развертываний Azure.</span><span class="sxs-lookup"><span data-stu-id="5f03a-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

