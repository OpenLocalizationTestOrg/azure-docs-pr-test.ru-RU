---
title: "Многоуровневая архитектура безопасности в средах службы приложений"
description: "Реализация многоуровневой архитектуры безопасности в средах службы приложений."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0fb02c13f99a8f4a46e0142c20da3b152c809b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="79b83-103">Реализация многоуровневой архитектуры безопасности со средами службы приложений</span><span class="sxs-lookup"><span data-stu-id="79b83-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="79b83-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="79b83-104">Overview</span></span>
<span data-ttu-id="79b83-105">Среды службы приложений предоставляют изолированную среду выполнения, развернутую в виртуальной сети. Поэтому разработчики могут создавать многоуровневую архитектуру безопасности, предусматривающую разные уровни доступа к сети для каждого физического уровня приложений.</span><span class="sxs-lookup"><span data-stu-id="79b83-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="79b83-106">Основная цель заключается в том, чтобы сделать невозможным общий доступ к внутреннему приложению API из Интернета, разрешив вызывать API только вышестоящими веб-приложениями.</span><span class="sxs-lookup"><span data-stu-id="79b83-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span></span>  <span data-ttu-id="79b83-107">В подсетях, содержащих среды службы приложений, могут использоваться [группы безопасности сети][NetworkSecurityGroups] для ограничения общего доступа к приложениям API.</span><span class="sxs-lookup"><span data-stu-id="79b83-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span></span>

<span data-ttu-id="79b83-108">На приведенной ниже схеме показан пример архитектуры с приложением на основе веб-API, развернутым в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="79b83-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="79b83-109">Три отдельных экземпляра веб-приложения, развернутые в трех отдельных средах службы приложений, выполняют внутренний вызов одного приложения веб-API.</span><span class="sxs-lookup"><span data-stu-id="79b83-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span></span>

![Концепция архитектуры][ConceptualArchitecture] 

<span data-ttu-id="79b83-111">Знак зеленого плюса указывает на то, что группа безопасности сети разрешает выполнять в подсети, содержащей apiase, входящие вызовы от вышестоящих веб-приложений, а также вызовы от самого приложения.</span><span class="sxs-lookup"><span data-stu-id="79b83-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="79b83-112">При этом та же группа безопасности сети явным образом запрещает доступ к общему входящему трафику из Интернета.</span><span class="sxs-lookup"><span data-stu-id="79b83-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span></span> 

<span data-ttu-id="79b83-113">В остальной части этого раздела описаны шаги по настройке группы безопасности сети в подсети, содержащей apiase.</span><span class="sxs-lookup"><span data-stu-id="79b83-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span></span>

## <a name="determining-the-network-behavior"></a><span data-ttu-id="79b83-114">Определение поведения сети</span><span class="sxs-lookup"><span data-stu-id="79b83-114">Determining the Network Behavior</span></span>
<span data-ttu-id="79b83-115">Чтобы узнать требуемые правила сетевой безопасности, вам необходимо определить, какие клиенты сети смогут обращаться к среде службы приложений, содержащей приложение API, а какие — будут заблокированы.</span><span class="sxs-lookup"><span data-stu-id="79b83-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span></span>

<span data-ttu-id="79b83-116">[Группы безопасности сети][NetworkSecurityGroups] применяются к подсетям, в которых также развертываются среды службы приложений. Поэтому содержащиеся в группе безопасности сети правила применяются ко **всем** приложениям, выполняющимся в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="79b83-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="79b83-117">Использование приведенного в этой статье примера архитектуры предполагает следующее. После того как группа безопасности сети будет применена к подсети, содержащей apiase, все приложения, выполняющиеся в среде службы приложений apiase, будут защищены этим же набором правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="79b83-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span></span> 

* <span data-ttu-id="79b83-118">**Определение исходящего IP-адреса вышестоящих вызывающих объектов.** Какой IP-адрес или какие IP-адреса у вышестоящих вызывающих объектов?</span><span class="sxs-lookup"><span data-stu-id="79b83-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span></span>  <span data-ttu-id="79b83-119">Эти адреса нужны для явного разрешения доступа в NSG.</span><span class="sxs-lookup"><span data-stu-id="79b83-119">These addresses will need to be explicitly allowed access in the NSG.</span></span>  <span data-ttu-id="79b83-120">Вызовы между средами службы приложений считаются интернет-вызовами. Это означает, что исходящему IP-адресу, назначенному каждому из трех вышестоящих приложений среды службы приложений, в NSG должен быть разрешен доступ для подсети apiase.</span><span class="sxs-lookup"><span data-stu-id="79b83-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span></span>   <span data-ttu-id="79b83-121">Дополнительные сведения об определении исходящего IP-адреса для приложений, выполняемых в среде службы приложений, см. в обзорной статье [Сетевая архитектура][NetworkArchitecture].</span><span class="sxs-lookup"><span data-stu-id="79b83-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="79b83-122">**Необходимо ли внутреннему приложению API вызывать самого себя?**</span><span class="sxs-lookup"><span data-stu-id="79b83-122">**Will the back-end API app need to call itself?**</span></span>  <span data-ttu-id="79b83-123">Есть один интересный сценарий, который часто упускают из виду: внутреннему приложению необходимо вызвать самого себя.</span><span class="sxs-lookup"><span data-stu-id="79b83-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span></span>  <span data-ttu-id="79b83-124">Если внутреннему приложению API в среде службы приложений необходимо обратиться к себе же, такой вызов также будет расценен как интернет-вызов.</span><span class="sxs-lookup"><span data-stu-id="79b83-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="79b83-125">В нашем примере архитектуры для этого также необходимо разрешить доступ от исходящего IP-адреса apiase среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="79b83-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-the-network-security-group"></a><span data-ttu-id="79b83-126">Настройка группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="79b83-126">Setting up the Network Security Group</span></span>
<span data-ttu-id="79b83-127">Когда набор исходящих IP-адресов станет известен, можно переходить к созданию группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="79b83-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span></span>  <span data-ttu-id="79b83-128">Группы безопасности сети можно создавать и для виртуальных сетей с Resource Manager, и для классических виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="79b83-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="79b83-129">В приведенных ниже примерах показано создание и настройка группы безопасности сети в классической виртуальной сети с помощью Powershell.</span><span class="sxs-lookup"><span data-stu-id="79b83-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="79b83-130">Так как в этом примере архитектуры среды расположены в Южно-Центральном регионе США, пустая группа NSG создается в этом регионе:</span><span class="sxs-lookup"><span data-stu-id="79b83-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="79b83-131">Сначала для инфраструктуры управления Azure добавляется одно явно разрешающее правило, как описано в статье, посвященной [управлению входящим трафиком][InboundTraffic] в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="79b83-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="79b83-132">Затем добавляются два правила, разрешающие вызовы HTTP и HTTPS из первой вышестоящей среды службы приложений (fe1ase).</span><span class="sxs-lookup"><span data-stu-id="79b83-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access to requests from the first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="79b83-133">То же самое выполняется для второй и третьей вышестоящих сред службы приложений (fe2ase и fe3ase).</span><span class="sxs-lookup"><span data-stu-id="79b83-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access to requests from the second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access to requests from the third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="79b83-134">Наконец, нужно предоставить доступ для исходящего IP-адреса среды службы приложений, в которую входит внутреннее приложение API, чтобы оно смогло вызывать само себя.</span><span class="sxs-lookup"><span data-stu-id="79b83-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on the apiase environment to call back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="79b83-135">Другие правила безопасности сети настраивать не нужно, так как у каждой группы NSG есть набор правил по умолчанию, блокирующий входящий доступ из Интернета по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="79b83-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span></span>

<span data-ttu-id="79b83-136">Полный список правил группы безопасности сети приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="79b83-136">The full list of rules in the network security group are shown below.</span></span>  <span data-ttu-id="79b83-137">Обратите внимание, как последнее правило (выделено) блокирует входящий доступ ото всех вызывающих объектов, отличных от тех, которым явно предоставлен доступ.</span><span class="sxs-lookup"><span data-stu-id="79b83-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Конфигурация NSG][NSGConfiguration] 

<span data-ttu-id="79b83-139">Последним шагом является применение группы NSG к подсети, которая содержит среду службы приложений apiase.</span><span class="sxs-lookup"><span data-stu-id="79b83-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span></span>  

     #Apply the NSG to the backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="79b83-140">После применения группы NSG к подсети вызывать среду apiase смогут только три вышестоящие среды службы приложений, а также среда службы приложений, содержащая серверную часть API.</span><span class="sxs-lookup"><span data-stu-id="79b83-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="79b83-141">Дополнительные ссылки и сведения</span><span class="sxs-lookup"><span data-stu-id="79b83-141">Additional Links and Information</span></span>
<span data-ttu-id="79b83-142">Все статьи и практические руководства, посвященные средам службы приложений, доступны в [файле сведений для сред службы приложений](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="79b83-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="79b83-143">Информация о [группах безопасности сети](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="79b83-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="79b83-144">Основные сведения об [исходящих IP-адресах][NetworkArchitecture] и средах службы приложений.</span><span class="sxs-lookup"><span data-stu-id="79b83-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="79b83-145">[Сетевые порты][InboundTraffic], используемые в средах службы приложений.</span><span class="sxs-lookup"><span data-stu-id="79b83-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
