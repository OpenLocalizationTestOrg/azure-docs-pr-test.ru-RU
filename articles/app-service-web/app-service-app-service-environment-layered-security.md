---
title: "aaaLayered архитектура безопасности с помощью среды службы приложений"
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
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="39890-103">Реализация многоуровневой архитектуры безопасности со средами службы приложений</span><span class="sxs-lookup"><span data-stu-id="39890-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="39890-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="39890-104">Overview</span></span>
<span data-ttu-id="39890-105">Среды службы приложений предоставляют изолированную среду выполнения, развернутую в виртуальной сети. Поэтому разработчики могут создавать многоуровневую архитектуру безопасности, предусматривающую разные уровни доступа к сети для каждого физического уровня приложений.</span><span class="sxs-lookup"><span data-stu-id="39890-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="39890-106">Общие желания toohide API назад интерфейсов из общего доступа к Интернету и только позволяет toobe API-интерфейсы, вызванных вышестоящего веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="39890-106">A common desire is toohide API back-ends from general Internet access, and only allow APIs toobe called by upstream web apps.</span></span>  <span data-ttu-id="39890-107">[Сетевые группы безопасности (Nsg)] [ NetworkSecurityGroups] может использоваться в подсетях, содержащую приложения tooAPI общего доступа toorestrict среды службы приложения.</span><span class="sxs-lookup"><span data-stu-id="39890-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments toorestrict public access tooAPI applications.</span></span>

<span data-ttu-id="39890-108">Hello приведенной ниже схеме показана архитектура примера с управлением WebAPI приложение, развернутое в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="39890-108">hello diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="39890-109">Три экземпляра приложения Интернета отдельно, развернутый на три отдельные среды службы приложения, сделать вызовы внутренней toohello же WebAPI приложения.</span><span class="sxs-lookup"><span data-stu-id="39890-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls toohello same WebAPI app.</span></span>

![Концепция архитектуры][ConceptualArchitecture] 

<span data-ttu-id="39890-111">Hello зеленый плюс указывают, hello сетевой группы безопасности в подсети hello, содержащая «apiase» позволяет входящих вызовов из hello вышестоящего веб-приложений, как хорошо вызовы от самого себя.</span><span class="sxs-lookup"><span data-stu-id="39890-111">hello green plus signs indicate that hello network security group on hello subnet containing "apiase" allows inbound calls from hello upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="39890-112">Однако hello явно отказывает в одной группе безопасности сети, доступ к toogeneral входящего трафика из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="39890-112">However hello same network security group explicitly denies access toogeneral inbound traffic from hello Internet.</span></span> 

<span data-ttu-id="39890-113">Hello оставшейся части этой статьи рассматриваются hello действия необходимые tooconfigure hello сетевой группы безопасности в подсети hello, содержащая «apiase».</span><span class="sxs-lookup"><span data-stu-id="39890-113">hello remainder of this topic walks through hello steps needed tooconfigure hello network security group on hello subnet containing "apiase".</span></span>

## <a name="determining-hello-network-behavior"></a><span data-ttu-id="39890-114">Определение hello неполадки в сети</span><span class="sxs-lookup"><span data-stu-id="39890-114">Determining hello Network Behavior</span></span>
<span data-ttu-id="39890-115">В порядке tooknow необходимости правила безопасности сети необходимо toodetermine, какие клиенты сети может tooreach среды службы приложений содержащего hello API приложение hello и какие клиенты будут заблокированы.</span><span class="sxs-lookup"><span data-stu-id="39890-115">In order tooknow what network security rules are needed, you need toodetermine which network clients will be allowed tooreach hello App Service Environment containing hello API app, and which clients will be blocked.</span></span>

<span data-ttu-id="39890-116">Так как [сетевых групп безопасности (Nsg)] [ NetworkSecurityGroups] , примененные toosubnets и развертываются среды службы приложения в подсетях, применяются правила hello, содержащихся в NSG слишком**все** приложения, работающие в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="39890-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied toosubnets, and App Service Environments are deployed into subnets, hello rules contained in an NSG apply too**all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="39890-117">С помощью hello образец архитектуры для данной статьи после группы безопасности сети применяется toohello подсети, где «apiase», все приложения, работающие на hello «apiase» среды службы приложений будет защищен hello же набор правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="39890-117">Using hello sample architecture for this article, once a network security group is applied toohello subnet containing "apiase", all apps running on hello "apiase" App Service Environment will be protected by hello same set of security rules.</span></span> 

* <span data-ttu-id="39890-118">**Определить hello исходящий IP-адрес вышестоящего вызывающим объектам:** возможности hello IP-адреса вышестоящего hello вызывающих объектов?</span><span class="sxs-lookup"><span data-stu-id="39890-118">**Determine hello outbound IP address of upstream callers:**  What is hello IP address or addresses of hello upstream callers?</span></span>  <span data-ttu-id="39890-119">Эти адреса должны явно разрешен доступ в hello NSG toobe.</span><span class="sxs-lookup"><span data-stu-id="39890-119">These addresses will need toobe explicitly allowed access in hello NSG.</span></span>  <span data-ttu-id="39890-120">Поскольку вызовы между среды службы приложения считаются вызовы «Internet», это означает hello исходящих IP-адреса, назначенного tooeach из hello три вышестоящего среды службы приложения требованиям toobe доступ разрешен в hello NSG для подсети «apiase» hello.</span><span class="sxs-lookup"><span data-stu-id="39890-120">Since calls between App Service Environments are considered "Internet" calls, this means hello outbound IP address assigned tooeach of hello three upstream App Service Environments needs toobe allowed access in hello NSG for hello "apiase" subnet.</span></span>   <span data-ttu-id="39890-121">Дополнительные сведения об определении hello исходящий IP-адрес приложения, выполняющиеся в среде службы приложений см. в разделе hello [архитектура сети] [ NetworkArchitecture] обзорную статью.</span><span class="sxs-lookup"><span data-stu-id="39890-121">For more details on determining hello outbound IP address for apps running in an App Service Environment see hello [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="39890-122">**Потребуется ли API приложение hello серверной части toocall сам?**</span><span class="sxs-lookup"><span data-stu-id="39890-122">**Will hello back-end API app need toocall itself?**</span></span>  <span data-ttu-id="39890-123">Иногда уделяется недостаточно внимания и неявные точки встречается hello целей toocall самого внутреннего приложения hello.</span><span class="sxs-lookup"><span data-stu-id="39890-123">A sometimes overlooked and subtle point is hello scenario where hello back-end application needs toocall itself.</span></span>  <span data-ttu-id="39890-124">Если в приложении API серверной части в среде службы приложений требуются toocall сам, это также обрабатываются как вызов «Интернет».</span><span class="sxs-lookup"><span data-stu-id="39890-124">If a back-end API application on an App Service Environment needs toocall itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="39890-125">В образец hello архитектуры для этого требуются доступ hello исходящий IP-адрес «apiase» среды службы приложений также hello.</span><span class="sxs-lookup"><span data-stu-id="39890-125">In hello sample architecture this requires allowing access from hello outbound IP address of hello "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-hello-network-security-group"></a><span data-ttu-id="39890-126">Настройка hello группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="39890-126">Setting up hello Network Security Group</span></span>
<span data-ttu-id="39890-127">После набора hello известны исходящий IP-адресов, hello следующим шагом является tooconstruct группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="39890-127">Once hello set of outbound IP addresses are known, hello next step is tooconstruct a network security group.</span></span>  <span data-ttu-id="39890-128">Группы безопасности сети можно создавать и для виртуальных сетей с Resource Manager, и для классических виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="39890-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="39890-129">Hello ниже примерах Создание и настройка NSG в классической виртуальной сети с помощью Powershell.</span><span class="sxs-lookup"><span data-stu-id="39890-129">hello examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="39890-130">Для архитектуры образец hello средах hello находятся в США, так что в этом регионе создается пустой NSG:</span><span class="sxs-lookup"><span data-stu-id="39890-130">For hello sample architecture, hello environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="39890-131">Сначала явно разрешить добавлено правило для hello инфраструктуры управления Azure, описанных в статье hello на [входящий трафик] [ InboundTraffic] для среды службы приложения.</span><span class="sxs-lookup"><span data-stu-id="39890-131">First an explicit allow rule is added for hello Azure management infrastructure as noted in hello article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="39890-132">После этого два правила будут добавлены tooallow HTTP и HTTPS вызовы из hello первый вышестоящего среды службы приложений («fe1ase»).</span><span class="sxs-lookup"><span data-stu-id="39890-132">Next, two rules are added tooallow HTTP and HTTPS calls from hello first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="39890-133">Здравствуйте, снова и повторите эти действия для второго и третьего вышестоящего приложения среды службы («fe2ase» и «fe3ase»).</span><span class="sxs-lookup"><span data-stu-id="39890-133">Rinse and repeat for hello second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="39890-134">Наконец предоставьте доступ toohello исходящих IP-адрес внутреннего интерфейса API hello среды службы приложений, чтобы он может выполнять обратный вызов в саму себя.</span><span class="sxs-lookup"><span data-stu-id="39890-134">Lastly, grant access toohello outbound IP address of hello back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="39890-135">Нет правил безопасности сети должны toobe настроен по умолчанию, поскольку каждый NSG имеет набор правил по умолчанию, блокирующие доступ входящего трафика из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="39890-135">No other network security rules need toobe configured because every NSG has a set of default rules that block inbound access from hello Internet by default.</span></span>

<span data-ttu-id="39890-136">Ниже приведены Hello полный список правил в группе безопасности сети hello.</span><span class="sxs-lookup"><span data-stu-id="39890-136">hello full list of rules in hello network security group are shown below.</span></span>  <span data-ttu-id="39890-137">Обратите внимание на то, как hello последнего правило, которое выделяется, блокирует доступ входящего трафика от всех вызывающих объектов, отличных от тех, которые явным образом предоставлен доступ.</span><span class="sxs-lookup"><span data-stu-id="39890-137">Note how hello last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Конфигурация NSG][NSGConfiguration] 

<span data-ttu-id="39890-139">последним шагом Hello является toohello подсети tooapply hello NSG, которая содержит apiase «hello» среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="39890-139">hello final step is tooapply hello NSG toohello subnet that contains hello "apiase" App Service Environment.</span></span>  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="39890-140">С подсетью toohello hello NSG применяется только hello три вышестоящего среды службы приложения hello содержащего hello среды службы приложений API серверной части, разрешены и toocall в среду «apiase» hello.</span><span class="sxs-lookup"><span data-stu-id="39890-140">With hello NSG applied toohello subnet, only hello three upstream App Service Environments, and hello App Service Environment containing hello API back-end, are allowed toocall into hello "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="39890-141">Дополнительные ссылки и сведения</span><span class="sxs-lookup"><span data-stu-id="39890-141">Additional Links and Information</span></span>
<span data-ttu-id="39890-142">Все статьи и как-для пользователя для среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="39890-142">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="39890-143">Информация о [группах безопасности сети](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="39890-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="39890-144">Основные сведения об [исходящих IP-адресах][NetworkArchitecture] и средах службы приложений.</span><span class="sxs-lookup"><span data-stu-id="39890-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="39890-145">[Сетевые порты][InboundTraffic], используемые в средах службы приложений.</span><span class="sxs-lookup"><span data-stu-id="39890-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
