---
title: "aaaCreate полное доменное имя для виртуальной Машины Linux в hello портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate полное доменное имя или полное доменное имя, для диспетчера ресурсов на основе виртуальной машины в hello портал Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a><span data-ttu-id="a5687-103">Создание полного доменного имени в hello портал Azure для виртуальной Машины Linux</span><span class="sxs-lookup"><span data-stu-id="a5687-103">Create a fully qualified domain name in hello Azure portal for a Linux VM</span></span>

<span data-ttu-id="a5687-104">При создании виртуальной машины (VM) в hello [портал Azure](https://portal.azure.com), открытому ресурсу IP для hello виртуальной машины создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="a5687-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="a5687-105">Можно использовать этот IP адрес tooremotely доступа hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a5687-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="a5687-106">Несмотря на то, что портал hello не приводит к созданию [полного доменного имени](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), или полное доменное имя, его можно добавить после hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a5687-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once hello VM is created.</span></span> <span data-ttu-id="a5687-107">В этой статье демонстрируется toocreate hello действия DNS-имя или полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="a5687-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="a5687-108">Создание полного доменного имени</span><span class="sxs-lookup"><span data-stu-id="a5687-108">Create a FQDN</span></span>
<span data-ttu-id="a5687-109">Для работы с руководством требуется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="a5687-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="a5687-110">При необходимости вы можете [создания виртуальной Машины на портале hello](quick-create-portal.md) или [с hello Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a5687-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with hello Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="a5687-111">Когда виртуальная машина будет готова, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a5687-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="a5687-112">Теперь можно подключиться удаленно toohello имя виртуальной Машины с помощью данной службы DNS как с `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="a5687-112">You can now connect remotely toohello VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5687-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5687-113">Next steps</span></span>
<span data-ttu-id="a5687-114">Теперь, когда у виртуальной машины имеется общедоступный IP-адрес и DNS-имя, можно развернуть общие программные платформы или службы, например nginx, MongoDB, Docker и т. д.</span><span class="sxs-lookup"><span data-stu-id="a5687-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="a5687-115">Изучите дополнительные сведения об [использовании Resource Manager](../../azure-resource-manager/resource-group-overview.md), чтобы получить советы по созданию развертываний Azure.</span><span class="sxs-lookup"><span data-stu-id="a5687-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

