---
title: "aaaList из toowhitelist URL-адреса и порты для Azure RemoteApp развернуты в виртуальной сети клиента | Документы Microsoft"
description: "Узнайте, какие порты и URL-адреса, вам потребуется tooconfigure для связи через Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="38c7f-103">Список URL-адреса и порты доступа toopermit для Azure RemoteApp развернуты в виртуальной сети клиента</span><span class="sxs-lookup"><span data-stu-id="38c7f-103">List of Ports and URLs toopermit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="38c7f-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="38c7f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="38c7f-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="38c7f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="38c7f-106">При развертывании коллекцию Azure RemoteApp облачной или гибридной в виртуальной сети (VNET), просмотрите следующие сведения о порте hello.</span><span class="sxs-lookup"><span data-stu-id="38c7f-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review hello following port information.</span></span> <span data-ttu-id="38c7f-107">Дополнительные сведения о виртуальных сетях см. в статье [Обзор виртуальной сети](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38c7f-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="38c7f-108">При создании ограничения трафика toohello виртуальных сетевых ресурсов в вашей коллекции группы безопасности сети (NSG), убедитесь, что следующие порты hello доступна и разрешенных в соответствии с политиками безопасности hello hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="38c7f-108">If you have created a network security group (NSG) restricting traffic toohello virtual network resources in your collection, make sure hello following ports are accessible and allowed through hello security policies on hello virtual network.</span></span> <span data-ttu-id="38c7f-109">Дополнительные сведения о группах безопасности сети см. в разделе [Группа безопасности сети (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="38c7f-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a><span data-ttu-id="38c7f-110">Azure RemoteApp подсеть должна включать конечные точки доступа toothese и URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="38c7f-110">Azure RemoteApp subnet needs access toothese endpoints and URLs:</span></span>
* <span data-ttu-id="38c7f-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="38c7f-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="38c7f-112">*.servicebus.net</span><span class="sxs-lookup"><span data-stu-id="38c7f-112">*.servicebus.net</span></span>
* <span data-ttu-id="38c7f-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="38c7f-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="38c7f-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="38c7f-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="38c7f-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="38c7f-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="38c7f-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="38c7f-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="38c7f-117">Исходящие: TCP: TCP: 443, 9351, 9352, 10101-10175.</span><span class="sxs-lookup"><span data-stu-id="38c7f-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="38c7f-118">Необязательно — UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="38c7f-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a><span data-ttu-id="38c7f-119">Azure RemoteApp клиенты должны получить доступ к URL-адреса и конечные точки toothese:</span><span class="sxs-lookup"><span data-stu-id="38c7f-119">Azure RemoteApp clients need access toothese endpoints and URLs:</span></span>
<span data-ttu-id="38c7f-120">Клиентами, которые я имею в виду hello настольных компьютеров, устройств и т.д. людей, используйте tooconnect toohello приложения развернуты в hello коллекции Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="38c7f-120">By clients I mean hello desktops, devices etc. that people use tooconnect toohello apps deployed in hello Azure RemoteApp collection.</span></span>

* <span data-ttu-id="38c7f-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="38c7f-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="38c7f-122">https://*.RemoteApp.windowsazure.com (hello дополнительные порты UDP, для этого адреса)</span><span class="sxs-lookup"><span data-stu-id="38c7f-122">https://*.remoteapp.windowsazure.com (hello optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="38c7f-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="38c7f-123">https://login.windows.net</span></span>  
* <span data-ttu-id="38c7f-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="38c7f-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="38c7f-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="38c7f-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="38c7f-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="38c7f-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="38c7f-127">Исходящие: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="38c7f-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="38c7f-128">(Необязательно) UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="38c7f-128">Optional - UDP: 3391</span></span> 

