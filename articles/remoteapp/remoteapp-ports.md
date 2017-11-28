---
title: "Список портов и URL-адресов для разрешения доступа к развернутым Azure RemoteApp в виртуальной сети клиента | Документация Майкрософт"
description: "Узнайте, какие порты и URL-адреса необходимо настроить для связи через Azure RemoteApp."
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
ms.openlocfilehash: c17ff8d5441ca92f7b893edb541a1e9730c2a847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="d1739-103">Список портов и URL-адресов для обеспечения доступа к развернутым Azure RemoteApp в виртуальной сети клиента</span><span class="sxs-lookup"><span data-stu-id="d1739-103">List of Ports and URLs to permit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d1739-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="d1739-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d1739-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="d1739-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d1739-106">Если вы развертываете облачную или гибридную коллекцию Azure RemoteApp в виртуальной сети (VNET), просмотрите приведенную ниже информацию о портах.</span><span class="sxs-lookup"><span data-stu-id="d1739-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review the following port information.</span></span> <span data-ttu-id="d1739-107">Дополнительные сведения о виртуальных сетях см. в статье [Обзор виртуальной сети](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1739-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="d1739-108">Если вы создали группу безопасности сети (NSG), ограничивающую трафик к ресурсам вашей виртуальной сети в коллекции, убедитесь, что приведенные ниже порты доступны и открыты посредством политик безопасности виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d1739-108">If you have created a network security group (NSG) restricting traffic to the virtual network resources in your collection, make sure the following ports are accessible and allowed through the security policies on the virtual network.</span></span> <span data-ttu-id="d1739-109">Дополнительные сведения о группах безопасности сети см. в разделе [Группа безопасности сети (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="d1739-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a><span data-ttu-id="d1739-110">Подсети Azure RemoteApp требуется доступ к этим конечным точкам и URL-адресам:</span><span class="sxs-lookup"><span data-stu-id="d1739-110">Azure RemoteApp subnet needs access to these endpoints and URLs:</span></span>
* <span data-ttu-id="d1739-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="d1739-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="d1739-112">*.servicebus.net</span><span class="sxs-lookup"><span data-stu-id="d1739-112">*.servicebus.net</span></span>
* <span data-ttu-id="d1739-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="d1739-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="d1739-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="d1739-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="d1739-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="d1739-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="d1739-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d1739-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="d1739-117">Исходящие: TCP: TCP: 443, 9351, 9352, 10101-10175.</span><span class="sxs-lookup"><span data-stu-id="d1739-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="d1739-118">Необязательно — UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="d1739-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a><span data-ttu-id="d1739-119">Клиентам Azure RemoteApp требуется доступ к этим конечным точкам и URL-адресам:</span><span class="sxs-lookup"><span data-stu-id="d1739-119">Azure RemoteApp clients need access to these endpoints and URLs:</span></span>
<span data-ttu-id="d1739-120">Под клиентами подразумеваются настольные системы, устройства и т. д., которые люди используют для подключения к приложениям, развернутым в коллекции Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d1739-120">By clients I mean the desktops, devices etc. that people use to connect to the apps deployed in the Azure RemoteApp collection.</span></span>

* <span data-ttu-id="d1739-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="d1739-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="d1739-122">https://*.remoteapp.windowsazure.com (необязательные UDP-порты для этого адреса)</span><span class="sxs-lookup"><span data-stu-id="d1739-122">https://*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="d1739-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="d1739-123">https://login.windows.net</span></span>  
* <span data-ttu-id="d1739-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d1739-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="d1739-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="d1739-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="d1739-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d1739-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="d1739-127">Исходящие: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="d1739-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="d1739-128">(Необязательно) UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="d1739-128">Optional - UDP: 3391</span></span> 

