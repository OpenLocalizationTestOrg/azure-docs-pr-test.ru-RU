---
title: "Пример: aaaDMZ построения DMZ tooProtect сетей с помощью брандмауэра, UDR и NSG | Документы Microsoft"
description: "Построение сети периметра с брандмауэром, определяемыми пользователем маршрутами и группами безопасности сети."
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="a9592-103">Пример 3 — построения DMZ tooProtect сетей с помощью брандмауэра, UDR и NSG</span><span class="sxs-lookup"><span data-stu-id="a9592-103">Example 3 – Build a DMZ tooProtect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="a9592-104">[Возвращает toohello страница лучшие рекомендации безопасности границ][HOME]</span><span class="sxs-lookup"><span data-stu-id="a9592-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="a9592-105">В этом примере будет создана сеть периметра (которая называется также DMZ, демилитаризованной зоной, или промежуточной подсетью) с брандмауэром, четырьмя серверами Windows Server, определяемыми пользователем маршрутами, IP-пересылкой и группами безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="a9592-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="a9592-106">Он также поможет выполнить каждого из соответствующих команд tooprovide hello более глубокого понимания каждого шага.</span><span class="sxs-lookup"><span data-stu-id="a9592-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="a9592-107">Имеется также сценарий трафика раздел tooprovide на подробные пошаговые трафик проходит через hello уровней защиты в hello DMZ.</span><span class="sxs-lookup"><span data-stu-id="a9592-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="a9592-108">Наконец, в разделе references hello hello полный код и должна toobuild инструкция этот tootest среды и эксперимента с помощью различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="a9592-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="a9592-109">![Двунаправленная сеть периметра с виртуальным сетевым устройством, группой безопасности сети и определяемыми пользователем маршрутами][1]</span><span class="sxs-lookup"><span data-stu-id="a9592-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="a9592-110">Настройка среды</span><span class="sxs-lookup"><span data-stu-id="a9592-110">Environment Setup</span></span>
<span data-ttu-id="a9592-111">В этом примере имеется подписка, содержащий hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a9592-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="a9592-112">три облачные службы: SecSvc001, FrontEnd001 и BackEnd001;</span><span class="sxs-lookup"><span data-stu-id="a9592-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="a9592-113">виртуальная сеть CorpNetwork с тремя подсетями (SecNet, FrontEnd и BackEnd);</span><span class="sxs-lookup"><span data-stu-id="a9592-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="a9592-114">Устройство виртуальной сети, в этом примере брандмауэр, подключены toohello SecNet подсети</span><span class="sxs-lookup"><span data-stu-id="a9592-114">A network virtual appliance, in this example a firewall, connected toohello SecNet subnet</span></span>
* <span data-ttu-id="a9592-115">сервер Windows Server, который представляет веб-сервер приложений (IIS01);</span><span class="sxs-lookup"><span data-stu-id="a9592-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="a9592-116">два сервера Windows Server, представляющих тыловые серверы приложений (AppVM01, AppVM02);</span><span class="sxs-lookup"><span data-stu-id="a9592-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="a9592-117">сервер Windows Server, который представляет DNS-сервер (DNS01).</span><span class="sxs-lookup"><span data-stu-id="a9592-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="a9592-118">В разделе references hello ниже имеется сценарий PowerShell, построит большая часть среды hello, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="a9592-118">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="a9592-119">Построение hello ВМ и виртуальными сетями, несмотря на то, что может быть выполнено с hello пример скрипта, не подробно описаны в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a9592-119">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="a9592-120">Среда toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-120">toobuild hello environment:</span></span>

1. <span data-ttu-id="a9592-121">Сохраните hello сетевой конфигурации XML-файл включаются в раздел ссылок hello (обновлено с именами, расположение и toomatch hello заданному IP адресов сценарий)</span><span class="sxs-lookup"><span data-stu-id="a9592-121">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="a9592-122">Переменные пользователя hello обновления в скрипт hello среды hello toomatch hello скрипта является toobe выполняться (подписок, имена служб, и т. д.)</span><span class="sxs-lookup"><span data-stu-id="a9592-122">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="a9592-123">Выполните сценарий hello в PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9592-123">Execute hello script in PowerShell</span></span>

<span data-ttu-id="a9592-124">**Примечание**: hello область — в hello сценарий PowerShell должен соответствовать hello область — в XML-файл конфигурации сети hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-124">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="a9592-125">После успешного выполнения сценария hello может быть переведена hello следующие шаги после сценария:</span><span class="sxs-lookup"><span data-stu-id="a9592-125">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="a9592-126">Настройка правил брандмауэра hello, это рассматривается в hello ниже раздел: Описание правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="a9592-126">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="a9592-127">При необходимости в разделе references hello являются двумя tooset сценарии hello веб-сервер и сервер приложений с простой web tooallow приложения, тестирование с помощью этой конфигурации сети Периметра.</span><span class="sxs-lookup"><span data-stu-id="a9592-127">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="a9592-128">После успешного выполнения сценария hello hello правила брандмауэра потребуется toobe завершена, это рассматривается в разделе hello: правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="a9592-128">Once hello script runs successfully hello firewall rules will need toobe completed, this is covered in hello section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="a9592-129">Определяемые пользователем маршруты</span><span class="sxs-lookup"><span data-stu-id="a9592-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="a9592-130">По умолчанию hello следующие маршруты системы определяются как:</span><span class="sxs-lookup"><span data-stu-id="a9592-130">By default, hello following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="a9592-131">Hello VNETLocal всегда является префиксы адресов определенные hello объекта hello виртуальной сети для этой конкретной сети (ie он изменится с tooVNet виртуальной сети в зависимости от способа определения каждой определенной виртуальной сети).</span><span class="sxs-lookup"><span data-stu-id="a9592-131">hello VNETLocal is always hello defined address prefix(es) of hello VNet for that specific network (ie it will change from VNet tooVNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="a9592-132">Здравствуйте, оставшиеся системы, статические маршруты и по умолчанию, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="a9592-132">hello remaining system routes are static and default as above.</span></span>

<span data-ttu-id="a9592-133">Как и для приоритетов маршруты обрабатываются через метод hello длинного соответствия префикса (LPM), таким образом hello наиболее конкретный маршрут в таблице hello бы применить tooa указанного адреса назначения.</span><span class="sxs-lookup"><span data-stu-id="a9592-133">As for priority, routes are processed via hello Longest Prefix Match (LPM) method, thus hello most specific route in hello table would apply tooa given destination address.</span></span>

<span data-ttu-id="a9592-134">Таким образом будет перенаправлен трафика (например toohello DNS01 сервер, 10.0.2.4), предназначенного для hello локальной сети (10.0.0.0/16) через назначения tooits hello виртуальной сети из-за toohello 10.0.0.0/16 маршрута.</span><span class="sxs-lookup"><span data-stu-id="a9592-134">Therefore, traffic (for example toohello DNS01 server, 10.0.2.4) intended for hello local network (10.0.0.0/16) would be routed across hello VNet tooits destination due toohello 10.0.0.0/16 route.</span></span> <span data-ttu-id="a9592-135">Другими словами для 10.0.2.4, hello 10.0.0.0/16 маршрута является наиболее конкретный маршрут hello, несмотря на то, что hello 10.0.0.0/8 и 0.0.0.0/0 также может применяться, но так как они менее точно не влияют на этого трафика.</span><span class="sxs-lookup"><span data-stu-id="a9592-135">In other words, for 10.0.2.4, hello 10.0.0.0/16 route is hello most specific route, even though hello 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="a9592-136">Таким образом hello трафика too10.0.2.4 бы следующего прыжка hello виртуальной локальной сети и просто маршрута toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="a9592-136">Thus hello traffic too10.0.2.4 would have a next hop of hello local VNet and simply route toohello destination.</span></span>

<span data-ttu-id="a9592-137">Если трафика был предназначен для 10.1.1.1, например, hello 10.0.0.0/16 маршрута не применяются, но hello 10.0.0.0/8 будет наиболее подходящим hello и hello трафик будет удалены («черный поставщик только») следующего прыжка hello имеет значение Null.</span><span class="sxs-lookup"><span data-stu-id="a9592-137">If traffic was intended for 10.1.1.1 for example, hello 10.0.0.0/16 route wouldn’t apply, but hello 10.0.0.0/8 would be hello most specific, and this hello traffic would be dropped (“black holed”) since hello next hop is Null.</span></span> 

<span data-ttu-id="a9592-138">Если hello назначения не был применен tooany префиксы Null hello или префиксы VNETLocal hello, то она будет следовать hello наименее конкретным маршрута, 0.0.0.0/0 и маршрутизироваться out toohello Интернета в качестве следующего прыжка hello и, следовательно, out edge Интернета в Azure.</span><span class="sxs-lookup"><span data-stu-id="a9592-138">If hello destination didn’t apply tooany of hello Null prefixes or hello VNETLocal prefixes, then it would follow hello least specific route, 0.0.0.0/0 and be routed out toohello Internet as hello next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="a9592-139">Если имеются два идентичных префикса в таблице маршрутов hello, hello Вот hello порядке приоритета на основе атрибута «источник» hello маршруты:</span><span class="sxs-lookup"><span data-stu-id="a9592-139">If there are two identical prefixes in hello route table, hello following is hello order of preference based on hello routes “source” attribute:</span></span>

1. <span data-ttu-id="a9592-140">«VirtualAppliance» = добавленные вручную toohello таблицы маршрутизации, определяемые пользователем</span><span class="sxs-lookup"><span data-stu-id="a9592-140">"VirtualAppliance" = A User Defined Route manually added toohello table</span></span>
2. <span data-ttu-id="a9592-141">«VPNGateway» = маршрут динамической (BGP при использовании гибридных сетях) добавлены динамические сетевым протоколом, эти маршруты может изменяться со временем как протоколом динамической hello автоматически отражает изменения в одноранговыми сети</span><span class="sxs-lookup"><span data-stu-id="a9592-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as hello dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="a9592-142">«Default» = hello системы маршруты, hello локальные статические записи виртуальной сети "и" hello, как показано в таблице маршрутов hello выше.</span><span class="sxs-lookup"><span data-stu-id="a9592-142">“Default” = hello System Routes, hello local VNet and hello static entries as shown in hello route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="a9592-143">Маршрутизации определенных пользователем (UDR) теперь можно использовать с ExpressRoute и VPN-шлюзов tooforce исходящего и входящего трафика между организациями трафик toobe перенаправленное tooa сети виртуальное устройство (уязвимости сети).</span><span class="sxs-lookup"><span data-stu-id="a9592-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways tooforce outbound and inbound cross-premises traffic toobe routed tooa network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-hello-local-routes"></a><span data-ttu-id="a9592-144">Создание локальных маршрутов hello</span><span class="sxs-lookup"><span data-stu-id="a9592-144">Creating hello local routes</span></span>
<span data-ttu-id="a9592-145">В этом примере требуются две таблицы маршрутизации, одному для каждого внешнего и внутреннего подсетей hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-145">In this example, two routing tables are needed, one each for hello Frontend and Backend subnets.</span></span> <span data-ttu-id="a9592-146">Каждая таблица загружается статические маршруты, соответствующие заданному подсети hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-146">Each table is loaded with static routes appropriate for hello given subnet.</span></span> <span data-ttu-id="a9592-147">В целях hello в этом примере каждая таблица имеет три маршруты:</span><span class="sxs-lookup"><span data-stu-id="a9592-147">For hello purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="a9592-148">Локальной подсети трафика со следующего прыжка определенные tooallow локальной подсети трафика toobypass hello брандмауэра</span><span class="sxs-lookup"><span data-stu-id="a9592-148">Local subnet traffic with no Next Hop defined tooallow local subnet traffic toobypass hello firewall</span></span>
2. <span data-ttu-id="a9592-149">Виртуального сетевого трафика с помощью следующего прыжка определяется как брандмауэр, он переопределяет правило по умолчанию hello и позволяющая локального tooroute трафика виртуальной сети напрямую</span><span class="sxs-lookup"><span data-stu-id="a9592-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides hello default rule that allows local VNet traffic tooroute directly</span></span>
3. <span data-ttu-id="a9592-150">Все остальные трафика (0-0) с помощью следующего прыжка определен как hello брандмауэра</span><span class="sxs-lookup"><span data-stu-id="a9592-150">All remaining traffic (0/0) with a Next Hop defined as hello firewall</span></span>

<span data-ttu-id="a9592-151">После создания таблицы маршрутизации hello это связанный tootheir подсетей.</span><span class="sxs-lookup"><span data-stu-id="a9592-151">Once hello routing tables are created they are bound tootheir subnets.</span></span> <span data-ttu-id="a9592-152">Для hello интерфейсной подсети таблицу маршрутизации после создания и привязки toohello подсети должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a9592-152">For hello Frontend subnet routing table, once created and bound toohello subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="a9592-153">В этом примере hello следующие команды, используемые toobuild таблицы маршрутов hello, добавьте маршрут определяемых пользователем и затем привязать подсети tooa таблицы маршрутов hello (Примечание; все элементы под начиная со знака доллара (например: $BESubnet), определенные пользователем переменные из сценария hello Hello справочном разделе этого документа):</span><span class="sxs-lookup"><span data-stu-id="a9592-153">For this example, hello following commands are used toobuild hello route table, add a user defined route, and then bind hello route table tooa subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="a9592-154">Первая таблица маршрутизации hello для базового должна быть создана.</span><span class="sxs-lookup"><span data-stu-id="a9592-154">First hello base routing table must be created.</span></span> <span data-ttu-id="a9592-155">Этот фрагмент показывает создание hello таблицы hello для внутренних подсети hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-155">This snippet shows hello creation of hello table for hello Backend subnet.</span></span> <span data-ttu-id="a9592-156">В сценарии hello для hello внешней подсети создается соответствующая таблица.</span><span class="sxs-lookup"><span data-stu-id="a9592-156">In hello script, a corresponding table is also created for hello Frontend subnet.</span></span>
   
     <span data-ttu-id="a9592-157">New-AzureRouteTable -Name $BERouteTableName \`</span><span class="sxs-lookup"><span data-stu-id="a9592-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="a9592-158">После создания таблицы маршрутов hello можно добавить определенные определяемые пользователем маршруты.</span><span class="sxs-lookup"><span data-stu-id="a9592-158">Once hello route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="a9592-159">В этом фрагмента весь трафик (0.0.0.0/0) будет проходить через hello виртуальное устройство (переменная, $VMIP [0] имеет используется toopass hello IP-адрес, назначенный при создании виртуального устройства hello, ранее в скрипте hello).</span><span class="sxs-lookup"><span data-stu-id="a9592-159">In this snipped, all traffic (0.0.0.0/0) will be routed through hello virtual appliance (a variable, $VMIP[0], is used toopass in hello IP address assigned when hello virtual appliance was created earlier in hello script).</span></span> <span data-ttu-id="a9592-160">В скрипте hello соответствующее правило создается также в таблице hello переднего плана.</span><span class="sxs-lookup"><span data-stu-id="a9592-160">In hello script, a corresponding rule is also created in hello Frontend table.</span></span>
   
     <span data-ttu-id="a9592-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="a9592-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="a9592-162">Hello выше записи маршрута будет переопределять маршрут «0.0.0.0/0» по умолчанию hello, но правило 10.0.0.0/16 по умолчанию hello, по-прежнему существующих, что позволит трафик в виртуальной сети tooroute hello непосредственно toohello назначения и toohello виртуальное устройство в сети.</span><span class="sxs-lookup"><span data-stu-id="a9592-162">hello above route entry will override hello default "0.0.0.0/0" route, but hello default 10.0.0.0/16 rule still existing which would allow traffic within hello VNet tooroute directly toohello destination and not toohello Network Virtual Appliance.</span></span> <span data-ttu-id="a9592-163">toocorrect, необходимо добавить это поведение hello выполните правило.</span><span class="sxs-lookup"><span data-stu-id="a9592-163">toocorrect this behavior hello follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="a9592-164">На этом этапе является выбор toobe внесены.</span><span class="sxs-lookup"><span data-stu-id="a9592-164">At this point there is a choice toobe made.</span></span> <span data-ttu-id="a9592-165">С hello выше двух маршрутов весь трафик будет направлять toohello брандмауэра для оценки, даже трафика в одной подсети.</span><span class="sxs-lookup"><span data-stu-id="a9592-165">With hello above two routes all traffic will route toohello firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="a9592-166">Это может оказаться целесообразным, однако tooallow трафик в подсети tooroute локально без участия hello брандмауэра можно добавить третий, определенных правил.</span><span class="sxs-lookup"><span data-stu-id="a9592-166">This may be desired, however tooallow traffic within a subnet tooroute locally without involvement from hello firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="a9592-167">Этот маршрут состояний, которые любой адрес destine для локальной подсети hello можно просто маршрутизации существует напрямую (NextHopType = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="a9592-167">This route states that any address destine for hello local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="a9592-168">Наконец с hello таблицу маршрутизации создаются и заполняются определяемые пользователем маршруты, hello таблица теперь должна быть привязанного tooa подсети.</span><span class="sxs-lookup"><span data-stu-id="a9592-168">Finally, with hello routing table created and populated with a user defined routes, hello table must now be bound tooa subnet.</span></span> <span data-ttu-id="a9592-169">В сценарий hello таблицы маршрутов hello переднего плана является привязанной toohello внешней подсети.</span><span class="sxs-lookup"><span data-stu-id="a9592-169">In hello script, hello front end route table is also bound toohello Frontend subnet.</span></span> <span data-ttu-id="a9592-170">Вот сценарий hello привязки для подсети hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a9592-170">Here is hello binding script for hello back end subnet.</span></span>
   
     <span data-ttu-id="a9592-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span><span class="sxs-lookup"><span data-stu-id="a9592-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="a9592-172">IP-пересылку</span><span class="sxs-lookup"><span data-stu-id="a9592-172">IP Forwarding</span></span>
<span data-ttu-id="a9592-173">Функция tooUDR помощник по поиску, — IP-пересылки.</span><span class="sxs-lookup"><span data-stu-id="a9592-173">A companion feature tooUDR, is IP Forwarding.</span></span> <span data-ttu-id="a9592-174">Это — параметр, позволяющий ему tooreceive трафик не было специально виртуального устройства обращаться toohello устройства и затем перешлите tooits конечного назначения этого трафика.</span><span class="sxs-lookup"><span data-stu-id="a9592-174">This is a setting on a Virtual Appliance that allows it tooreceive traffic not specifically addressed toohello appliance and then forward that traffic tooits ultimate destination.</span></span>

<span data-ttu-id="a9592-175">Например если трафик от AppVM01 делает запрос серверу DNS01 toohello UDR бы маршрутизацию toohello брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="a9592-175">As an example, if traffic from AppVM01 makes a request toohello DNS01 server, UDR would route this toohello firewall.</span></span> <span data-ttu-id="a9592-176">С IP-пересылка включена hello трафик для назначения DNS01 hello (10.0.2.4) будет принято устройством hello (10.0.0.4) и затем пересылаются конечного назначения tooits (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="a9592-176">With IP Forwarding enabled, hello traffic for hello DNS01 destination (10.0.2.4) will be accepted by hello appliance (10.0.0.4) and then forwarded tooits ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="a9592-177">Без IP-пересылка включена hello брандмауэра трафик будет не будут приниматься с устройством hello даже при таблицы маршрутов hello брандмауэра hello как hello следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="a9592-177">Without IP Forwarding enabled on hello Firewall, traffic would not be accepted by hello appliance even though hello route table has hello firewall as hello next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a9592-178">Это tooenable критические tooremember IP-пересылки в сочетании с определенных маршрутизации пользователя.</span><span class="sxs-lookup"><span data-stu-id="a9592-178">It’s critical tooremember tooenable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="a9592-179">IP-пересылка настраивается с помощью единственной команды. Настройку можно выполнить во время создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a9592-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="a9592-180">Для hello потока следующий фрагмент кода hello пример — концу hello скрипт hello и группируются с hello UDR команды:</span><span class="sxs-lookup"><span data-stu-id="a9592-180">For hello flow of this example hello code snippet is towards hello end of hello script and grouped with hello UDR commands:</span></span>

1. <span data-ttu-id="a9592-181">Вызова hello экземпляр виртуальной Машины, который является вашей виртуальной машины, в этом случае hello брандмауэра и включить IP-пересылку (Примечание; любой элемент в начало красным знаком доллара (например: $VMName[0]) является определяемой пользователем переменной из скрипта hello в справочном разделе hello этого документа.</span><span class="sxs-lookup"><span data-stu-id="a9592-181">Call hello VM instance that is your virtual appliance, hello firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="a9592-182">Здравствуйте ноль в квадратные скобки, [0], представляет hello первая виртуальная машина в массиве hello виртуальных машин, для hello пример сценария toowork без изменений, брандмауэра hello hello, должна быть первой виртуальной Машины (VM 0)):</span><span class="sxs-lookup"><span data-stu-id="a9592-182">hello zero in brackets, [0], represents hello first VM in hello array of VMs, for hello example script toowork without modification, hello first VM (VM 0) must be hello firewall):</span></span>
   
     <span data-ttu-id="a9592-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span><span class="sxs-lookup"><span data-stu-id="a9592-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="a9592-184">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="a9592-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="a9592-185">В этом примере создается группа безопасности сети, после чего в нее загружается одно правило.</span><span class="sxs-lookup"><span data-stu-id="a9592-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="a9592-186">Эта группа будет привязан только toohello внешнего и внутреннего подсети (не hello SecNet).</span><span class="sxs-lookup"><span data-stu-id="a9592-186">This group is then bound only toohello Frontend and Backend subnets (not hello SecNet).</span></span> <span data-ttu-id="a9592-187">Декларативно, строится hello следующие правила:</span><span class="sxs-lookup"><span data-stu-id="a9592-187">Declaratively hello following rule is being built:</span></span>

1. <span data-ttu-id="a9592-188">Любой трафик (все порты) из Интернета toohello hello запрещен всей виртуальной сети (все подсети)</span><span class="sxs-lookup"><span data-stu-id="a9592-188">Any traffic (all ports) from hello Internet toohello entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="a9592-189">В этом примере используются группы безопасности сети, но его основной целью является создание дополнительного уровня защиты от неправильной настройки вручную.</span><span class="sxs-lookup"><span data-stu-id="a9592-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="a9592-190">Мы хотим tooblock все входящий трафик от hello internet tooeither hello переднего плана или подсети серверной части, трафик только должен проходить hello брандмауэра toohello SecNet подсети (и затем, если соответствующие на toohello клиентской или серверной подсети).</span><span class="sxs-lookup"><span data-stu-id="a9592-190">We want tooblock all inbound traffic from hello internet tooeither hello Frontend or Backend subnets, traffic should only flow through hello SecNet subnet toohello firewall (and then if appropriate on toohello Frontend or Backend subnets).</span></span> <span data-ttu-id="a9592-191">Кроме того с правилами UDR hello в месте, любой трафик, который сделать hello клиентской или серверной подсетей будет направлять out toohello брандмауэра (спасибо tooUDR).</span><span class="sxs-lookup"><span data-stu-id="a9592-191">Plus, with hello UDR rules in place, any traffic that did make it into hello Frontend or Backend subnets would be directed out toohello firewall (thanks tooUDR).</span></span> <span data-ttu-id="a9592-192">брандмауэр Hello увидят это поток асимметричного и уменьшится hello исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="a9592-192">hello firewall would see this as an asymmetric flow and would drop hello outbound traffic.</span></span> <span data-ttu-id="a9592-193">Таким образом существует три уровня безопасности защищающее hello переднего плана и серверной подсети; (1) не открытые конечные точки на hello FrontEnd001 и BackEnd001 облачные службы, (2) Nsg Запрет трафика из Интернета, брандмауэр hello (3), удаление асимметричного трафика hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-193">Thus there are three layers of security protecting hello Frontend and Backend subnets; 1) no open endpoints on hello FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from hello Internet, 3) hello firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="a9592-194">Один интересный момент относительно hello сетевой группы безопасности в этом примере является, содержащий хотя бы одно правило, показанный ниже, toodeny Интернет трафика toohello всей виртуальной сеть включающие hello безопасности подсети.</span><span class="sxs-lookup"><span data-stu-id="a9592-194">One interesting point regarding hello Network Security Group in this example is that it contains only one rule, shown below, which is toodeny internet traffic toohello entire virtual network which would include hello Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="a9592-195">Тем не менее, поскольку hello NSG — только привязан toohello интерфейсной и серверной подсетей, hello правило не обрабатывается на трафик входящих подключений подсети toohello безопасности.</span><span class="sxs-lookup"><span data-stu-id="a9592-195">However, since hello NSG is only bound toohello Frontend and Backend subnets, hello rule isn’t processed on traffic inbound toohello Security subnet.</span></span> <span data-ttu-id="a9592-196">В результате несмотря на то, что правило NSG hello говорит не tooany трафика Интернет-адрес на hello виртуальной сети, поскольку приветствия NSG никогда не был привязан toohello безопасности подсети, трафик будет проходить подсети toohello безопасности.</span><span class="sxs-lookup"><span data-stu-id="a9592-196">As a result, even though hello NSG rule says no Internet traffic tooany address on hello VNet, because hello NSG was never bound toohello Security subnet, traffic will flow toohello Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="a9592-197">Правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="a9592-197">Firewall Rules</span></span>
<span data-ttu-id="a9592-198">На брандмауэре hello правила перенаправления потребуется создать toobe.</span><span class="sxs-lookup"><span data-stu-id="a9592-198">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="a9592-199">Так как брандмауэр hello трафика блокировки или пересылки все входящие, Исходящие и внутри виртуальной сети требуется много правил брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="a9592-199">Since hello firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="a9592-200">Кроме того, весь входящий трафик столкнутся hello службы безопасности общедоступный IP-адрес (по различным портам), toobe обрабатываемых hello брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="a9592-200">Also, all inbound traffic will hit hello Security Service public IP address (on different ports), toobe processed by hello firewall.</span></span> <span data-ttu-id="a9592-201">Лучший способ — toodiagram hello логических потоков перед настройкой подсети hello и доработку tooavoid правила брандмауэра позже.</span><span class="sxs-lookup"><span data-stu-id="a9592-201">A best practice is toodiagram hello logical flows before setting up hello subnets and firewall rules tooavoid rework later.</span></span> <span data-ttu-id="a9592-202">Hello на этом рисунке — это логическое представление hello правила брандмауэра для этого примера:</span><span class="sxs-lookup"><span data-stu-id="a9592-202">hello following figure is a logical view of hello firewall rules for this example:</span></span>

<span data-ttu-id="a9592-203">![Логическое представление hello правила брандмауэра][2]</span><span class="sxs-lookup"><span data-stu-id="a9592-203">![Logical View of hello Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="a9592-204">На основании hello используется виртуальное устройство в сети, будет зависеть порты управления hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-204">Based on hello Network Virtual Appliance used, hello management ports will vary.</span></span> <span data-ttu-id="a9592-205">В этом примере брандмауэр Barracuda NextGen Firewall использует порты 22, 801 и 807.</span><span class="sxs-lookup"><span data-stu-id="a9592-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="a9592-206">Обратитесь к hello устройства поставщика документации toofind hello точное порты, используемые для управления hello устройства, используемого.</span><span class="sxs-lookup"><span data-stu-id="a9592-206">Please consult hello appliance vendor documentation toofind hello exact ports used for management of hello device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="a9592-207">Описание логического правила</span><span class="sxs-lookup"><span data-stu-id="a9592-207">Logical Rule Description</span></span>
<span data-ttu-id="a9592-208">Hello логической схеме выше подсети hello безопасности не отображаются, поскольку hello брандмауэра является ресурсом только hello в этой подсети, и на этой схеме показан правила брандмауэра hello и как они логически разрешить или запретить трафик, поступающий и не hello фактический перенаправленное путь.</span><span class="sxs-lookup"><span data-stu-id="a9592-208">In hello logical diagram above, hello security subnet is not shown since hello firewall is hello only resource on that subnet, and this diagram is showing hello firewall rules and how they logically allow or deny traffic flows and not hello actual routed path.</span></span> <span data-ttu-id="a9592-209">Кроме того, hello внешними портами, выбранный для hello трафик RDP, выше диапазоны портов (8014 — 8026) и были выбранного toosomewhat соответствовать hello последние два октета hello локальный IP-адрес для упрощения восприятия (например адрес локального сервера 10.0.1.4 связан с внешний порт 8014), однако все более порты неконфликтующее могут быть использованы.</span><span class="sxs-lookup"><span data-stu-id="a9592-209">Also, hello external ports selected for hello RDP traffic are higher ranged ports (8014 – 8026) and were selected toosomewhat align with hello last two octets of hello local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="a9592-210">В этом примере нам нужно 7 типов правил. Их описание приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="a9592-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="a9592-211">Внешние правила (для входящего трафика):</span><span class="sxs-lookup"><span data-stu-id="a9592-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="a9592-212">Правило брандмауэра управления: Это правило перенаправления приложения разрешает трафик порты управления toohello toopass hello сети виртуальных устройств.</span><span class="sxs-lookup"><span data-stu-id="a9592-212">Firewall Management Rule: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance.</span></span>
  2. <span data-ttu-id="a9592-213">Правила протокола удаленного рабочего СТОЛА (для каждого сервера windows): эти четыре правила, по одному для каждого сервера, будет разрешить управление hello отдельных серверах с помощью протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="a9592-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of hello individual servers via RDP.</span></span> <span data-ttu-id="a9592-214">Это также может быть собраны в одно правило, в зависимости от возможностей hello hello сети виртуальной машины используется.</span><span class="sxs-lookup"><span data-stu-id="a9592-214">This could also be bundled into one rule depending on hello capabilities of hello Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="a9592-215">Правила трафика приложения: Существует два правила трафика приложения hello сначала для hello внешнего интерфейса веб-трафика и hello второй для трафика серверной части hello (например, веб-сервера toodata уровня).</span><span class="sxs-lookup"><span data-stu-id="a9592-215">Application Traffic Rules: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="a9592-216">Конфигурация Hello из этих правил будет зависеть от hello сетевую архитектуру (где располагаются серверов) и трафик, поступающий (hello какие направление трафик проходит и порты, используемые).</span><span class="sxs-lookup"><span data-stu-id="a9592-216">hello configuration of these rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="a9592-217">Первое правило Hello позволит hello hello фактического приложения трафика tooreach сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="a9592-217">hello first rule will allow hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="a9592-218">Хотя hello другие правила позволяют для обеспечения безопасности, управления и т. д., правила, приложения, что разрешить внешние tooaccess пользователям или службам приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-218">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="a9592-219">В этом примере нет одного веб-сервера на порт 80, и таким образом одно приложение правило брандмауэра будет перенаправлять входящий трафик toohello внешний IP-адрес, toohello web внутренний IP-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="a9592-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span> <span data-ttu-id="a9592-220">Hello перенаправление трафика сеанса будет NAT имеет toohello внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="a9592-220">hello redirected traffic session would be NAT’d toohello internal server.</span></span>
     * <span data-ttu-id="a9592-221">Hello является второе правило трафика приложения hello tootalk сервера toohello AppVM01 tooallow hello серверной части правила веб-сервера (но не AppVM02) через любой порт.</span><span class="sxs-lookup"><span data-stu-id="a9592-221">hello second Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="a9592-222">Внутренние правила (для внутреннего трафика виртуальной сети)</span><span class="sxs-lookup"><span data-stu-id="a9592-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="a9592-223">Исходящие tooInternet правило: это правило разрешает трафик от какой-либо сети toopass toohello выбранной сети.</span><span class="sxs-lookup"><span data-stu-id="a9592-223">Outbound tooInternet Rule: This rule will allow traffic from any network toopass toohello selected networks.</span></span> <span data-ttu-id="a9592-224">Это правило обычно является правилом по умолчанию уже на брандмауэре hello, но в отключенном состоянии.</span><span class="sxs-lookup"><span data-stu-id="a9592-224">This rule is usually a default rule already on hello firewall, but in a disabled state.</span></span> <span data-ttu-id="a9592-225">В нашем примере это правило следует активировать.</span><span class="sxs-lookup"><span data-stu-id="a9592-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="a9592-226">Правило DNS: Это правило разрешает только DNS (порт 53) трафика toopass toohello DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="a9592-226">DNS Rule: This rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="a9592-227">Для этой среды, заблокирован большая часть трафика из toohello переднего плана hello серверной части это правило разрешает специально DNS из любой локальной подсети.</span><span class="sxs-lookup"><span data-stu-id="a9592-227">For this environment most traffic from hello Frontend toohello Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="a9592-228">Подсети tooSubnet правило: это правило является tooallow любой сервер обратной hello внутренний сервер tooany tooconnect подсети в подсети hello внешнего интерфейса (но не hello обратного).</span><span class="sxs-lookup"><span data-stu-id="a9592-228">Subnet tooSubnet Rule: This rule is tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet (but not hello reverse).</span></span>
* <span data-ttu-id="a9592-229">Резервный правило (для трафика, который не удовлетворяет любому из hello выше):</span><span class="sxs-lookup"><span data-stu-id="a9592-229">Fail-safe Rule (for traffic that doesn’t meet any of hello above):</span></span>
  1. <span data-ttu-id="a9592-230">Запретить все правила трафика: Это всегда должны содержать hello окончательного правило (с точки зрения приоритета) и таким образом Если трафик проходит происходит сбой toomatch любой hello предшествующий правила, которые они будут удалены с помощью этого правила.</span><span class="sxs-lookup"><span data-stu-id="a9592-230">Deny All Traffic Rule: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="a9592-231">Это правило обычно уже установлено по умолчанию и активировано, поэтому не требует дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="a9592-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="a9592-232">На hello второе правило трафика приложения любой порт может легко этого примера, в hello реальные сценарии наиболее конкретный порт а также диапазоны адресов должны быть уязвимость hello используется tooreduce данного правила.</span><span class="sxs-lookup"><span data-stu-id="a9592-232">On hello second application traffic rule, any port is allowed for easy of this example, in a real scenario hello most specific port and address ranges should be used tooreduce hello attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="a9592-233">После создания всех hello выше правила важно tooreview hello приоритета трафика tooensure каждого правила будет разрешаться или запрещаться желаемым образом.</span><span class="sxs-lookup"><span data-stu-id="a9592-233">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="a9592-234">В этом примере hello правила следуют в порядке приоритета.</span><span class="sxs-lookup"><span data-stu-id="a9592-234">For this example, hello rules are in priority order.</span></span> <span data-ttu-id="a9592-235">Это легко toobe hello брандмауэра из-за правил, упорядоченных toomis был заблокирован.</span><span class="sxs-lookup"><span data-stu-id="a9592-235">It's easy toobe locked out of hello firewall due toomis-ordered rules.</span></span> <span data-ttu-id="a9592-236">Как минимум убедитесь, что hello управления сам брандмауэр hello всегда соответствует hello абсолютный наивысший приоритет правила.</span><span class="sxs-lookup"><span data-stu-id="a9592-236">At a minimum, ensure hello management for hello firewall itself is always hello absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="a9592-237">Предварительные требования для правил</span><span class="sxs-lookup"><span data-stu-id="a9592-237">Rule Prerequisites</span></span>
<span data-ttu-id="a9592-238">Один необходимых компонентов для брандмауэра hello работающей виртуальной машины hello являются общедоступными конечными точками.</span><span class="sxs-lookup"><span data-stu-id="a9592-238">One prerequisite for hello Virtual Machine running hello firewall are public endpoints.</span></span> <span data-ttu-id="a9592-239">Трафик tooprocess брандмауэра hello hello соответствующие общедоступные конечные точки должны быть открыты.</span><span class="sxs-lookup"><span data-stu-id="a9592-239">For hello firewall tooprocess traffic hello appropriate public endpoints must be open.</span></span> <span data-ttu-id="a9592-240">Существует три типа трафика в этом примере; (1) управления трафика toocontrol hello брандмауэра и правила брандмауэра, серверов windows hello toocontrol трафик RDP (2) и трафика (3) приложения.</span><span class="sxs-lookup"><span data-stu-id="a9592-240">There are three types of traffic in this example; 1) Management traffic toocontrol hello firewall and firewall rules, 2) RDP traffic toocontrol hello windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="a9592-241">Это hello три столбца типов трафика в hello верхней половины логическое представление выше правила брандмауэра hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-241">These are hello three columns of traffic types in hello upper half of logical view of hello firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9592-242">Ключа takeway здесь — tooremember, **все** трафик будет поступать через брандмауэр hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-242">A key takeway here is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="a9592-243">Так tooremote рабочего стола toohello IIS01 server, несмотря на то, что это hello Front End облачной службы, так и в подсети hello переднего плана, tooaccess этот сервер будет необходимо tooRDP toohello брандмауэра на порт 8014 и подождите hello брандмауэра tooroute hello RDP запроса внутри toohello IIS01 порт протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="a9592-243">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="a9592-244">Здравствуйте, портал Azure «подключиться», кнопка не будет работать, поскольку нет прямой путь tooIIS01 протокола удаленного рабочего СТОЛА (как можно увидеть hello портала).</span><span class="sxs-lookup"><span data-stu-id="a9592-244">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="a9592-245">Это означает все соединения с hello Интернета будут toohello службы безопасности и номером порта, например secscv001.cloudapp.net:xxxx (Справочник по hello выше схемы для сопоставления hello внешний порт и внутренний IP-адрес и порт).</span><span class="sxs-lookup"><span data-stu-id="a9592-245">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference hello above diagram for hello mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="a9592-246">Может быть открыт либо во время создания виртуальной Машины hello или post сборки, как показано ниже в этом фрагменте кода и сделать в примере сценария hello конечной точки (Примечание; все элемента, начинающиеся со знака доллара (например: $VMName[$i]) является определяемой пользователем переменной из скрипта hello в hello referen CE раздел этого документа.</span><span class="sxs-lookup"><span data-stu-id="a9592-246">An endpoint can be opened either at hello time of VM creation or post build as is done in hello example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="a9592-247">Hello «$i» в квадратные скобки, [$i] представляет номер массива hello определенную виртуальную Машину в массиве виртуальные машины):</span><span class="sxs-lookup"><span data-stu-id="a9592-247">hello “$i” in brackets, [$i], represents hello array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="a9592-248">Несмотря на то, что здесь не четко показано из-за toohello использование переменных, но конечные точки являются **только** открывается на hello безопасности облачной службы.</span><span class="sxs-lookup"><span data-stu-id="a9592-248">Although not clearly shown here due toohello use of variables, but endpoints are **only** opened on hello Security Cloud Service.</span></span> <span data-ttu-id="a9592-249">Это tooensure обработки весь входящий трафик (маршрутизироваться, NAT сброшен) брандмауэром hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-249">This is tooensure that all inbound traffic is handled (routed, NAT'd, dropped) by hello firewall.</span></span>

<span data-ttu-id="a9592-250">Клиент управления будет требуется toobe установлен брандмауэр hello toomanage ПК и создавать hello конфигурациях.</span><span class="sxs-lookup"><span data-stu-id="a9592-250">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="a9592-251">См. документации из брандмауэр (или другие Уязвимости) поставщика hello как toomanage hello устройства.</span><span class="sxs-lookup"><span data-stu-id="a9592-251">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="a9592-252">Hello оставшейся части этого раздела и следующего раздела hello, создания правил брандмауэра, описывается hello конфигурации брандмауэра hello, через hello клиент управления поставщиков (т. е. не hello портал Azure или PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a9592-252">hello remainder of this section and hello next section, Firewall Rules Creation, will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="a9592-253">Инструкции по загрузки клиента и подключении toohello Barracuda используется в этом примере можно найти здесь: [Barracuda NG администратора](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="a9592-253">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="a9592-254">После входа на брандмауэре hello, но до создания правила брандмауэра, существует два класса готовности объекта, которые могут облегчить создание правил hello; Объекты, сеть и службы.</span><span class="sxs-lookup"><span data-stu-id="a9592-254">Once logged onto hello firewall but before creating firewall rules, there are two prerequisite object classes that can make creating hello rules easier; Network & Service objects.</span></span>

<span data-ttu-id="a9592-255">В этом примере три объекта именованной сети следует определенных (одно для hello внешней подсети и подсети hello серверной части, также объект сети для IP-адреса hello hello DNS-сервера).</span><span class="sxs-lookup"><span data-stu-id="a9592-255">For this example, three named network objects should be defined (one for hello Frontend subnet and hello Backend subnet, also a network object for hello IP address of hello DNS server).</span></span> <span data-ttu-id="a9592-256">toocreate именованной сети; начиная с панели мониторинга клиент Barracuda NG Admin hello, перейдите на вкладку toohello конфигурации, в hello рабочей конфигурации раздела выберите набор правил, нажмите кнопку «Сети» в меню объектов брандмауэра hello, нажмите нажмите кнопку "Создать" в меню Правка сетей hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-256">toocreate a named network; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Networks” under hello Firewall Objects menu, then click New in hello Edit Networks menu.</span></span> <span data-ttu-id="a9592-257">Hello объекта сети теперь можно создать, добавив приветствия имен и префиксов hello:</span><span class="sxs-lookup"><span data-stu-id="a9592-257">hello network object can now be created, by adding hello name and hello prefix:</span></span>

<span data-ttu-id="a9592-258">![Создание сетевого объекта FrontEnd][3]</span><span class="sxs-lookup"><span data-stu-id="a9592-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="a9592-259">Это создаст именованной сети для подсети hello переднего плана, похожих объектов, создаваемых для hello также подсети серверной части.</span><span class="sxs-lookup"><span data-stu-id="a9592-259">This will create a named network for hello FrontEnd subnet, a similar object should be created for hello BackEnd subnet as well.</span></span> <span data-ttu-id="a9592-260">Теперь hello подсетей можно легко ссылаться по имени в правилах брандмауэра hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-260">Now hello subnets can be more easily referenced by name in hello firewall rules.</span></span>

<span data-ttu-id="a9592-261">Для hello объекта сервера DNS:</span><span class="sxs-lookup"><span data-stu-id="a9592-261">For hello DNS Server Object:</span></span>

<span data-ttu-id="a9592-262">![Создание объекта сервера DNS][4]</span><span class="sxs-lookup"><span data-stu-id="a9592-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="a9592-263">Это ссылка на один IP адресов будут использоваться в правиле "DNS" Далее в документе hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-263">This single IP address reference will be utilized in a DNS rule later in hello document.</span></span>

<span data-ttu-id="a9592-264">Hello второй необходимые объекты являются объектами службы.</span><span class="sxs-lookup"><span data-stu-id="a9592-264">hello second prerequisite objects are Services objects.</span></span> <span data-ttu-id="a9592-265">Будет представляют Привет порты подключения протокола удаленного рабочего СТОЛА для каждого сервера.</span><span class="sxs-lookup"><span data-stu-id="a9592-265">These will represent hello RDP connection ports for each server.</span></span> <span data-ttu-id="a9592-266">Поскольку hello существующего объекта службы протокола удаленного рабочего СТОЛА RDP-порту по умолчанию связанного toohello, 3389, новые службы могут создаваться tooallow трафика из hello внешние порты (8014 8026).</span><span class="sxs-lookup"><span data-stu-id="a9592-266">Since hello existing RDP service object is bound toohello default RDP port, 3389, new Services can be created tooallow traffic from hello external ports (8014-8026).</span></span> <span data-ttu-id="a9592-267">новые порты Hello также могут быть добавлены toohello существующую службу протокола удаленного рабочего СТОЛА, но для простоты демонстрации можно создать отдельное правило для каждого сервера.</span><span class="sxs-lookup"><span data-stu-id="a9592-267">hello new ports could also be added toohello existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="a9592-268">toocreate новое правило протокола удаленного рабочего СТОЛА для сервера; начиная с панели мониторинга hello Barracuda NG администратора клиента, перейдите toohello вкладка конфигурации, в hello рабочей конфигурации раздела щелкните набор правил, затем щелкните «Службы» в группе hello меню объектов брандмауэра, прокрутите вниз список hello служб и выберите hello Служба «Протокола удаленного рабочего СТОЛА».</span><span class="sxs-lookup"><span data-stu-id="a9592-268">toocreate a new RDP rule for a server; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Services” under hello Firewall Objects menu, scroll down hello list of services and select hello “RDP” service.</span></span> <span data-ttu-id="a9592-269">Щелкните правой кнопкой мыши и выберите копию, затем щелкните правой кнопкой мыши и выберите команду «Вставить».</span><span class="sxs-lookup"><span data-stu-id="a9592-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="a9592-270">Теперь у нас есть объект службы RDP-Copy1, который можно редактировать.</span><span class="sxs-lookup"><span data-stu-id="a9592-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="a9592-271">Щелкните правой кнопкой мыши Copy1 протокола удаленного рабочего СТОЛА и выберите изменение, hello изменить объект службы, окно появится, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="a9592-271">Right-click RDP-Copy1 and select Edit, hello Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="a9592-272">![Копия правила RDP по умолчанию][5]</span><span class="sxs-lookup"><span data-stu-id="a9592-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="a9592-273">Hello значения затем могут быть hello измененного toorepresent службы протокола удаленного рабочего СТОЛА для конкретного сервера.</span><span class="sxs-lookup"><span data-stu-id="a9592-273">hello values can then be edited toorepresent hello RDP service for a specific server.</span></span> <span data-ttu-id="a9592-274">Для hello AppVM01 выше по умолчанию правило протокола удаленного рабочего СТОЛА следует измененный tooreflect новое имя службы, описание, и внешний порт протокола удаленного рабочего СТОЛА используется при hello схема на рис. 8 (Примечание: hello порты изменяются с hello по умолчанию RDP 3389 внешний порт toohello используется для этого конкретного сервера, в случае, когда hello AppVM01 hello внешний порт является 8025) hello измененные службы показан ниже:</span><span class="sxs-lookup"><span data-stu-id="a9592-274">For AppVM01 hello above default RDP rule should be modified tooreflect a new Service Name, Description, and external RDP Port used in hello Figure 8 diagram (Note: hello ports are changed from hello RDP default of 3389 toohello external port being used for this specific server, in hello case of AppVM01 hello external Port is 8025) hello modified service is shown below:</span></span>

<span data-ttu-id="a9592-275">![Правило AppVM01][6]</span><span class="sxs-lookup"><span data-stu-id="a9592-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="a9592-276">Этот процесс должен быть повторяющихся toocreate службы протокола удаленного рабочего СТОЛА для hello оставшихся серверов. AppVM02 DNS01 и IIS01.</span><span class="sxs-lookup"><span data-stu-id="a9592-276">This process must be repeated toocreate RDP Services for hello remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="a9592-277">Создание Hello этих служб сделает создание правила hello проще и более очевидным в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-277">hello creation of these Services will make hello Rule creation simpler and more obvious in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="a9592-278">Служба протокола удаленного рабочего СТОЛА для hello брандмауэра не требуется по двум причинам; (1) первый hello брандмауэра виртуальной Машины — это изображение под управлением Linux, поэтому SSH будет использоваться порт 22 для управления виртуальными Машинами вместо протокола удаленного рабочего СТОЛА и (2) порт 22, а два других портов управления разрешены в hello описанных ниже tooallow для управления подключением первое правило управления.</span><span class="sxs-lookup"><span data-stu-id="a9592-278">An RDP service for hello Firewall is not needed for two reasons; 1) first hello firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in hello first management rule described below tooallow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="a9592-279">Создание правил брандмауэра</span><span class="sxs-lookup"><span data-stu-id="a9592-279">Firewall Rules Creation</span></span>
<span data-ttu-id="a9592-280">В этом примере используется три типа правил брандмауэра. Все они имеют собственные значки.</span><span class="sxs-lookup"><span data-stu-id="a9592-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="a9592-281">Правила перенаправления приложения Hello: ![значка перенаправления приложения][7]</span><span class="sxs-lookup"><span data-stu-id="a9592-281">hello Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="a9592-282">правило NAT назначения Hello: ![NAT значок назначения][8]</span><span class="sxs-lookup"><span data-stu-id="a9592-282">hello Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="a9592-283">правила этапа Hello: ![передать значок][9]</span><span class="sxs-lookup"><span data-stu-id="a9592-283">hello Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="a9592-284">Дополнительные сведения об этих правил можно найти на веб-сайте Barracuda hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-284">More information on these rules can be found at hello Barracuda web site.</span></span>

<span data-ttu-id="a9592-285">toocreate hello правилам (или проверить существующие правила по умолчанию), начиная с панели мониторинга клиент Barracuda NG Admin hello, перейдите на вкладку Конфигурация toohello, в hello рабочей конфигурации нажмите кнопку набора правил.</span><span class="sxs-lookup"><span data-stu-id="a9592-285">toocreate hello following rules (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="a9592-286">Вызывается сетку, «Main правила» будет отображаться hello существующие активные и неактивные правила на этот брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="a9592-286">A grid called, “Main Rules” will show hello existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="a9592-287">Верхний правый угол hello сетки является небольшой, зеленый «+», выберите элемент этого toocreate новое правило (Примечание: брандмауэра «заблокирована» для изменения, если кнопки помечен «Lock» и, не удается toocreate или изменение правил, нажмите эту кнопку, отображается слишком «разблокировать» hello правило se t и разрешить изменение).</span><span class="sxs-lookup"><span data-stu-id="a9592-287">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello rule set and allow editing).</span></span> <span data-ttu-id="a9592-288">При желании tooedit существующее правило, выберите это правило, щелкните правой кнопкой мыши и выберите команду Изменить правило.</span><span class="sxs-lookup"><span data-stu-id="a9592-288">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="a9592-289">После создания или изменения правил, они должны быть выполнены toohello брандмауэра и затем активируется, если этого не сделать hello правило, изменения не вступят в силу.</span><span class="sxs-lookup"><span data-stu-id="a9592-289">Once your rules are created and/or modified, they must be pushed toohello firewall and then activated, if this is not done hello rule changes will not take effect.</span></span> <span data-ttu-id="a9592-290">Hello принудительной отправки и активации процесс описан ниже описания правил hello сведения.</span><span class="sxs-lookup"><span data-stu-id="a9592-290">hello push and activation process is described below hello details rule descriptions.</span></span>

<span data-ttu-id="a9592-291">особенности Hello каждое правило требуется toocomplete в этом примере описаны следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a9592-291">hello specifics of each rule required toocomplete this example are described as follows:</span></span>

* <span data-ttu-id="a9592-292">**Правило управления брандмауэра**: это приложение перенаправлено правило разрешает трафик порты управления toohello toopass hello сети виртуальных устройств, в этом примере брандмауэр Barracuda NextGen.</span><span class="sxs-lookup"><span data-stu-id="a9592-292">**Firewall Management Rule**: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="a9592-293">порты для управления Hello: 801, 807 и при необходимости 22.</span><span class="sxs-lookup"><span data-stu-id="a9592-293">hello management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="a9592-294">Hello внешние и внутренние порты являются hello же (т. е. без преобразования порт).</span><span class="sxs-lookup"><span data-stu-id="a9592-294">hello external and internal ports are hello same (i.e. no port translation).</span></span> <span data-ttu-id="a9592-295">SETUP-MGMT-ACCESS является правилом по умолчанию и включено по умолчанию (в брандмауэре Barracuda NextGen Firewall версии 6.1).</span><span class="sxs-lookup"><span data-stu-id="a9592-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="a9592-296">![Правило управления брандмауэром][10]</span><span class="sxs-lookup"><span data-stu-id="a9592-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="a9592-297">Hello источника адресного пространства для этого правила может быть любым, если hello известны управления диапазоны IP-адресов, уменьшая этой области также уменьшает порты управления toohello поверхности атаки hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-297">hello source address space in this rule is Any, if hello management IP address ranges are known, reducing this scope would also reduce hello attack surface toohello management ports.</span></span>
> 
> 

* <span data-ttu-id="a9592-298">**Правила протокола удаленного рабочего СТОЛА**: правила преобразования сетевых адресов эти назначения будет разрешить управление hello отдельных серверах с помощью протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="a9592-298">**RDP Rules**:  These Destination NAT rules will allow management of hello individual servers via RDP.</span></span>
  <span data-ttu-id="a9592-299">Существует четыре toocreate критического поля, необходимые этого правила:</span><span class="sxs-lookup"><span data-stu-id="a9592-299">There are four critical fields needed toocreate this rule:</span></span>
  
  1. <span data-ttu-id="a9592-300">Источник — tooallow RDP в любом месте hello ссылку «Любой» используется в hello исходного поля.</span><span class="sxs-lookup"><span data-stu-id="a9592-300">Source – tooallow RDP from anywhere, hello reference “Any” is used in hello Source field.</span></span>
  2. <span data-ttu-id="a9592-301">Службы — использовать соответствующий объект службы создан ранее, в данном случае «AppVM01 RDP» приветствия, внешними портами hello перенаправить toohello серверы локальный IP-адрес и tooport 3386 (порт протокола удаленного рабочего СТОЛА по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="a9592-301">Service – use hello appropriate Service Object created earlier, in this case “AppVM01 RDP”, hello external ports redirect toohello servers local IP address and tooport 3386 (hello default RDP port).</span></span> <span data-ttu-id="a9592-302">Это конкретных правило предназначено для tooAppVM01 доступ RDP.</span><span class="sxs-lookup"><span data-stu-id="a9592-302">This specific rule is for RDP access tooAppVM01.</span></span>
  3. <span data-ttu-id="a9592-303">Назначение — должно представлять hello *локальных портов на брандмауэре hello*, «DCHP 1 локальный IP-адрес» или eth0 при использовании статических IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a9592-303">Destination – should be hello *local port on hello firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="a9592-304">Порядковый номер Hello (eth0, eth1, и т. д.) может отличаться, если устройство вашей сети имеет несколько локальных интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="a9592-304">hello ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="a9592-305">Это hello порт брандмауэра hello отправки из (может быть hello же, как получение порта hello), hello фактическое перенаправленное назначения находится в поля со списком целевой hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-305">This is hello port hello firewall is sending out from (may be hello same as hello receiving port), hello actual routed destination is in hello Target List field.</span></span>
  4. <span data-ttu-id="a9592-306">Перенаправление — в этом разделе приведен виртуальное устройство hello где tooultimately перенаправление этого трафика.</span><span class="sxs-lookup"><span data-stu-id="a9592-306">Redirection – this section tells hello virtual appliance where tooultimately redirect this traffic.</span></span> <span data-ttu-id="a9592-307">Простейший перенаправление Hello является tooplace hello IP и порта (необязательно) в поле списка целевой hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-307">hello simplest redirection is tooplace hello IP and Port (optional) in hello Target List field.</span></span> <span data-ttu-id="a9592-308">Если порт не используется hello конечный порт на входящий запрос hello будет использовать (ie без преобразования), если порт назначается hello порт также будет NAT вместе с hello IP по адресу.</span><span class="sxs-lookup"><span data-stu-id="a9592-308">If no port is used hello destination port on hello inbound request will be used (ie no translation), if a port is designated hello port will also be NAT’d along with hello IP address.</span></span>
     
     <span data-ttu-id="a9592-309">![Правило RDP брандмауэра][11]</span><span class="sxs-lookup"><span data-stu-id="a9592-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="a9592-310">Всего четыре правила RDP потребуется создать toobe:</span><span class="sxs-lookup"><span data-stu-id="a9592-310">A total of four RDP rules will need toobe created:</span></span> 
     
     | <span data-ttu-id="a9592-311">Имя правила</span><span class="sxs-lookup"><span data-stu-id="a9592-311">Rule Name</span></span> | <span data-ttu-id="a9592-312">сервер;</span><span class="sxs-lookup"><span data-stu-id="a9592-312">Server</span></span> | <span data-ttu-id="a9592-313">служба</span><span class="sxs-lookup"><span data-stu-id="a9592-313">Service</span></span> | <span data-ttu-id="a9592-314">Целевой список</span><span class="sxs-lookup"><span data-stu-id="a9592-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="a9592-315">RDP-to-IIS01</span><span class="sxs-lookup"><span data-stu-id="a9592-315">RDP-to-IIS01</span></span> |<span data-ttu-id="a9592-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="a9592-316">IIS01</span></span> |<span data-ttu-id="a9592-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="a9592-317">IIS01 RDP</span></span> |<span data-ttu-id="a9592-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="a9592-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="a9592-319">RDP-to-DNS01</span><span class="sxs-lookup"><span data-stu-id="a9592-319">RDP-to-DNS01</span></span> |<span data-ttu-id="a9592-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="a9592-320">DNS01</span></span> |<span data-ttu-id="a9592-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="a9592-321">DNS01 RDP</span></span> |<span data-ttu-id="a9592-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="a9592-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="a9592-323">RDP-to-AppVM01</span><span class="sxs-lookup"><span data-stu-id="a9592-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="a9592-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="a9592-324">AppVM01</span></span> |<span data-ttu-id="a9592-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="a9592-325">AppVM01 RDP</span></span> |<span data-ttu-id="a9592-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="a9592-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="a9592-327">RDP-to-AppVM02</span><span class="sxs-lookup"><span data-stu-id="a9592-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="a9592-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="a9592-328">AppVM02</span></span> |<span data-ttu-id="a9592-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="a9592-329">AppVm02 RDP</span></span> |<span data-ttu-id="a9592-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="a9592-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="a9592-331">Сужение области hello hello источника и поля службы позволяет снизить уязвимость hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-331">Narrowing down hello scope of hello Source and Service fields will reduce hello attack surface.</span></span> <span data-ttu-id="a9592-332">следует использовать Hello наиболее ограниченную область, которая позволит функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="a9592-332">hello most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="a9592-333">**Применение правил трафика**: существует два правила трафика приложения hello сначала для hello внешнего интерфейса веб-трафика и hello второй для трафика серверной части hello (например, веб-сервера toodata уровень).</span><span class="sxs-lookup"><span data-stu-id="a9592-333">**Application Traffic Rules**: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="a9592-334">Эти правила будут зависеть от hello сетевой архитектуры, (где располагаются серверов) и трафик, поступающий (hello какие направление трафик проходит и порты, используемые).</span><span class="sxs-lookup"><span data-stu-id="a9592-334">These rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="a9592-335">Сначала рассматриваются — hello правило внешнего интерфейса для веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="a9592-335">First discussed is hello front end rule for web traffic:</span></span>
  
    <span data-ttu-id="a9592-336">![Веб-правило брандмауэра][12]</span><span class="sxs-lookup"><span data-stu-id="a9592-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="a9592-337">Это правило NAT назначения разрешает hello hello фактического приложения трафика tooreach сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="a9592-337">This Destination NAT rule allows hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="a9592-338">Хотя hello другие правила позволяют для обеспечения безопасности, управления и т. д., правила, приложения, что разрешить внешние tooaccess пользователям или службам приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-338">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="a9592-339">В этом примере нет одного веб-сервера на порт 80, и таким образом hello одно приложение правило брандмауэра будет перенаправлять входящий трафик toohello внешний IP-адрес, toohello web внутренний IP-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="a9592-339">For this example, there is a single web server on port 80, thus hello single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span>
  
    <span data-ttu-id="a9592-340">**Примечание**: что нет порта, назначенного в поля со списком целевой hello, таким образом hello входящий порт 80 (или 443 для hello выбранной службой) будет использоваться в перенаправлении hello hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="a9592-340">**Note**: that there is no port assigned in hello Target List field, thus hello inbound port 80 (or 443 for hello Service selected) will be used in hello redirection of hello web server.</span></span> <span data-ttu-id="a9592-341">Если hello веб-сервер прослушивает другой порт, например 8080, поля со списком целевой hello может быть обновленные too10.0.1.4:8080 tooallow для hello также перенаправление портов.</span><span class="sxs-lookup"><span data-stu-id="a9592-341">If hello web server is listening on a different port, for example port 8080, hello Target List field could be updated too10.0.1.4:8080 tooallow for hello Port redirection as well.</span></span>
  
    <span data-ttu-id="a9592-342">Hello следующего правила трафика приложения — через любую службу hello tootalk сервера toohello AppVM01 tooallow hello серверной части правила веб-сервера (но не AppVM02):</span><span class="sxs-lookup"><span data-stu-id="a9592-342">hello next Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="a9592-343">![Правило AppVM01 брандмауэра][13]</span><span class="sxs-lookup"><span data-stu-id="a9592-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="a9592-344">Это правило проход дает любой сервер IIS на hello интерфейсной подсети tooreach hello AppVM01 (IP-адрес 10.0.2.5) через любой порт, используя любой протокол tooaccess данные, необходимые для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-344">This Pass rule allows any IIS server on hello Frontend subnet tooreach hello AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol tooaccess data needed by hello web application.</span></span>
  
    <span data-ttu-id="a9592-345">На этом снимке экрана "\<явные dest\>» используется в toosignify поле назначения hello 10.0.2.5 hello назначения.</span><span class="sxs-lookup"><span data-stu-id="a9592-345">In this screen shot an "\<explicit-dest\>" is used in hello Destination field toosignify 10.0.2.5 as hello destination.</span></span> <span data-ttu-id="a9592-346">Это может быть либо явные показанное или с именем сетевой объект (как это было сделано в предварительных требованиях hello hello DNS-сервера).</span><span class="sxs-lookup"><span data-stu-id="a9592-346">This could be either explicit as shown or a named Network Object (as was done in hello prerequisites for hello DNS server).</span></span> <span data-ttu-id="a9592-347">Это копирование администратора toohello hello брандмауэра будет использоваться метод toowhich.</span><span class="sxs-lookup"><span data-stu-id="a9592-347">This is up toohello administrator of hello firewall as toowhich method will be used.</span></span> <span data-ttu-id="a9592-348">Дважды щелкните первую пустую строку hello под tooadd 10.0.2.5 как конечный Explict \<явные dest\> и введите адрес hello в окне приветствия, будет отображена.</span><span class="sxs-lookup"><span data-stu-id="a9592-348">tooadd 10.0.2.5 as an Explict Desitnation, double-click on hello first blank row under \<explicit-dest\> and enter hello address in hello window that pops up.</span></span>
  
    <span data-ttu-id="a9592-349">С этим правилом передать не NAT необходим, так как это внутренний трафик, чтобы можно было задать слишком hello метод подключения «Нет SNAT».</span><span class="sxs-lookup"><span data-stu-id="a9592-349">With this Pass Rule, no NAT is needed since this is internal traffic, so hello Connection Method can be set too"No SNAT".</span></span>
  
    <span data-ttu-id="a9592-350">**Примечание**: hello исходную сеть в этом правиле, любой ресурс на hello внешней подсети, если будет существовать только один, либо известных определенное число веб-серверы, объект сетевого ресурса может быть создан toobe более конкретные toothose точного IP-адреса вместо Hello всей подсети переднего плана.</span><span class="sxs-lookup"><span data-stu-id="a9592-350">**Note**: hello Source network in this rule is any resource on hello FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created toobe more specific toothose exact IP addresses instead of hello entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="a9592-351">Это правило использует службу hello «Любой» toomake toosetup простой пример приложения hello и использовать, это также позволит ICMPv4 (ping) в одно правило.</span><span class="sxs-lookup"><span data-stu-id="a9592-351">This rule uses hello service “Any” toomake hello sample application easier toosetup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="a9592-352">Однако так делать не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="a9592-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="a9592-353">Hello порты и протоколы («службы») должно быть возможно минимальное узкую toohello, что позволяет операции tooreduce приложения hello возможных направлений атак через эту границу.</span><span class="sxs-lookup"><span data-stu-id="a9592-353">hello ports and protocols (“Services”) should be narrowed toohello minimum possible that allows application operation tooreduce hello attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="a9592-354">Несмотря на то, что это правило показывает ссылку явную dest используется, целостный подход следует использовать в конфигурации брандмауэра hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout hello firewall configuration.</span></span> <span data-ttu-id="a9592-355">Рекомендуется, hello именованный объект сети будет использоваться в для упрощения чтения и поддержки.</span><span class="sxs-lookup"><span data-stu-id="a9592-355">It is recommended that hello named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="a9592-356">явные dest Hello используемые здесь только tooshow альтернативные ссылки метод и обычно не рекомендуется (особенно для сложных конфигураций).</span><span class="sxs-lookup"><span data-stu-id="a9592-356">hello explicit-dest is used here only tooshow an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="a9592-357">**Исходящие tooInternet правило**: передайте это правило разрешает трафик из любого источника сети toopass toohello выбранного назначения сетей.</span><span class="sxs-lookup"><span data-stu-id="a9592-357">**Outbound tooInternet Rule**: This Pass rule will allow traffic from any Source network toopass toohello selected Destination networks.</span></span> <span data-ttu-id="a9592-358">Это правило является правилом по умолчанию обычно уже брандмауэр Barracuda NextGen hello, но находится в отключенном состоянии.</span><span class="sxs-lookup"><span data-stu-id="a9592-358">This rule is a default rule usually already on hello Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="a9592-359">Щелкните правой кнопкой мыши на это правило может обращаться к команда активировать правило hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-359">Right-clicking on this rule can access hello Activate Rule command.</span></span> <span data-ttu-id="a9592-360">правило Hello, показанный здесь был измененный tooadd hello двух локальных подсетях, созданных как ссылки hello необходимых компонентов из раздела этого документа toohello исходный атрибут данного правила.</span><span class="sxs-lookup"><span data-stu-id="a9592-360">hello rule shown here has been modified tooadd hello two local subnets that were created as references in hello prerequisite section of this document toohello Source attribute of this rule.</span></span>
  
    <span data-ttu-id="a9592-361">![Правило исходящего трафика брандмауэра][14]</span><span class="sxs-lookup"><span data-stu-id="a9592-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="a9592-362">**Правило DNS**: передайте это правило разрешает только DNS (порт 53) трафика toopass toohello DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="a9592-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="a9592-363">Для этой среды, заблокирован большая часть трафика из toohello переднего плана hello серверной части это правило, в частности, позволяет DNS.</span><span class="sxs-lookup"><span data-stu-id="a9592-363">For this environment most traffic from hello FrontEnd toohello BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="a9592-364">![Правило DNS брандмауэра][15]</span><span class="sxs-lookup"><span data-stu-id="a9592-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="a9592-365">**Примечание**: на этом экране включено однократного hello метод подключения.</span><span class="sxs-lookup"><span data-stu-id="a9592-365">**Note**: In this screen shot hello Connection Method is included.</span></span> <span data-ttu-id="a9592-366">Так как это правило предназначено для внутреннего IP toointernal IP-адрес трафика, не NATing не требуется, это hello задан метод подключения слишком «Нет SNAT» для этого правила этапа.</span><span class="sxs-lookup"><span data-stu-id="a9592-366">Because this rule is for internal IP toointernal IP address traffic, no NATing is required, this hello Connection Method is set too“No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="a9592-367">**Подсети tooSubnet правило**: передайте это правило является правилом по умолчанию, который был активирован и измененный tooallow на любом сервере в hello обратно внутренний сервер tooany tooconnect подсети на hello подсети переднего плана.</span><span class="sxs-lookup"><span data-stu-id="a9592-367">**Subnet tooSubnet Rule**: This Pass rule is a default rule that has been activated and modified tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet.</span></span> <span data-ttu-id="a9592-368">Это правило не все внутренний трафик, чтобы hello метод подключения можно задать tooNo SNAT.</span><span class="sxs-lookup"><span data-stu-id="a9592-368">This rule is all internal traffic so hello Connection Method can be set tooNo SNAT.</span></span>
  
    <span data-ttu-id="a9592-369">![Правило брандмауэра для внутреннего трафика виртуальной сети][16]</span><span class="sxs-lookup"><span data-stu-id="a9592-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="a9592-370">**Примечание**: hello двунаправленные флажок не установлен (и поддерживается не возврата большинство правил), это важно для этого правила в том, что она делает это правило «один письмом», соединение может быть инициирован с hello серверной части подсети toohello интерфейсную сеть но не hello обратное.</span><span class="sxs-lookup"><span data-stu-id="a9592-370">**Note**: hello Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from hello back end subnet toohello front end network, but not hello reverse.</span></span> <span data-ttu-id="a9592-371">Если установить флажок, правило будет разрешать двунаправленный трафик, а в нашей логической схеме это не требуется.</span><span class="sxs-lookup"><span data-stu-id="a9592-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="a9592-372">**Запретить все правила трафика**: это всегда должно быть правило окончательного hello (с точки зрения приоритета), и таким образом, если трафик проходит toomatch завершается с ошибкой любой из предыдущих правил hello они будут удалены с помощью этого правила.</span><span class="sxs-lookup"><span data-stu-id="a9592-372">**Deny All Traffic Rule**: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="a9592-373">Это правило обычно уже установлено по умолчанию и активировано, поэтому не требует дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="a9592-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="a9592-374">![Правило запрета брандмауэра][17]</span><span class="sxs-lookup"><span data-stu-id="a9592-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9592-375">После создания всех hello выше правила важно tooreview hello приоритета трафика tooensure каждого правила будет разрешаться или запрещаться желаемым образом.</span><span class="sxs-lookup"><span data-stu-id="a9592-375">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="a9592-376">В этом примере hello правила являются в порядке их отображения в hello сетки Main правил в клиент управления Barracuda hello переадресации hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-376">For this example, hello rules are in hello order they should appear in hello Main Grid of forwarding rules in hello Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="a9592-377">Активация правил</span><span class="sxs-lookup"><span data-stu-id="a9592-377">Rule Activation</span></span>
<span data-ttu-id="a9592-378">Спецификации hello изменить ruleset toohello схемы логики hello, hello ruleset должен быть отправлен toohello брандмауэра и затем активируется.</span><span class="sxs-lookup"><span data-stu-id="a9592-378">With hello ruleset modified toohello specification of hello logic diagram, hello ruleset must be uploaded toohello firewall and then activated.</span></span>

<span data-ttu-id="a9592-379">![Активация правила брандмауэра][18]</span><span class="sxs-lookup"><span data-stu-id="a9592-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="a9592-380">В правом верхнем углу hello клиент управления hello являются кластера кнопок.</span><span class="sxs-lookup"><span data-stu-id="a9592-380">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="a9592-381">Щелкните toohello «Изменения отправить «hello кнопка toosend hello изменены правила брандмауэра, а затем нажмите кнопку «Активировать» hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-381">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="a9592-382">Hello активации из набора правил брандмауэра hello с этой сборкой среды пример завершена.</span><span class="sxs-lookup"><span data-stu-id="a9592-382">With hello activation of hello firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="a9592-383">Варианты прохождения трафика</span><span class="sxs-lookup"><span data-stu-id="a9592-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a9592-384">Ключа takeway — tooremember, **все** трафик будет поступать через брандмауэр hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-384">A key takeway is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="a9592-385">Так tooremote рабочего стола toohello IIS01 server, несмотря на то, что это hello Front End облачной службы, так и в подсети hello переднего плана, tooaccess этот сервер будет необходимо tooRDP toohello брандмауэра на порт 8014 и подождите hello брандмауэра tooroute hello RDP запроса внутри toohello IIS01 порт протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="a9592-385">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="a9592-386">Здравствуйте, портал Azure «подключиться», кнопка не будет работать, поскольку нет прямой путь tooIIS01 протокола удаленного рабочего СТОЛА (как можно увидеть hello портала).</span><span class="sxs-lookup"><span data-stu-id="a9592-386">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="a9592-387">Это означает все соединения с hello Интернета будут toohello службы безопасности и номером порта, например secscv001.cloudapp.net:xxxx.</span><span class="sxs-lookup"><span data-stu-id="a9592-387">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="a9592-388">В этих сценариях hello следующие правила брандмауэра должно быть на месте:</span><span class="sxs-lookup"><span data-stu-id="a9592-388">For these scenarios, hello following firewall rules should be in place:</span></span>

1. <span data-ttu-id="a9592-389">Управление брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="a9592-389">Firewall Management</span></span>
2. <span data-ttu-id="a9592-390">TooIIS01 протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="a9592-390">RDP tooIIS01</span></span>
3. <span data-ttu-id="a9592-391">TooDNS01 протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="a9592-391">RDP tooDNS01</span></span>
4. <span data-ttu-id="a9592-392">TooAppVM01 протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="a9592-392">RDP tooAppVM01</span></span>
5. <span data-ttu-id="a9592-393">TooAppVM02 протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="a9592-393">RDP tooAppVM02</span></span>
6. <span data-ttu-id="a9592-394">Toohello трафика приложения Web</span><span class="sxs-lookup"><span data-stu-id="a9592-394">App Traffic toohello Web</span></span>
7. <span data-ttu-id="a9592-395">TooAppVM01 трафика приложения</span><span class="sxs-lookup"><span data-stu-id="a9592-395">App Traffic tooAppVM01</span></span>
8. <span data-ttu-id="a9592-396">Исходящие toohello Интернета</span><span class="sxs-lookup"><span data-stu-id="a9592-396">Outbound toohello Internet</span></span>
9. <span data-ttu-id="a9592-397">TooDNS01 переднего плана</span><span class="sxs-lookup"><span data-stu-id="a9592-397">Frontend tooDNS01</span></span>
10. <span data-ttu-id="a9592-398">Трафик внутри подсети (только для серверной части toofront конец)</span><span class="sxs-lookup"><span data-stu-id="a9592-398">Intra-Subnet Traffic (back end toofront end only)</span></span>
11. <span data-ttu-id="a9592-399">Запрет любого трафика.</span><span class="sxs-lookup"><span data-stu-id="a9592-399">Deny All</span></span>

<span data-ttu-id="a9592-400">набор правил брандмауэра фактическое Hello скорее всего будет иметь множество правил в toothese сложения, hello правила на любом брандмауэре данного также будет иметь различные приоритеты чисел, чем другие перечисленные здесь hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-400">hello actual firewall ruleset will most likely have many other rules in addition toothese, hello rules on any given firewall will also have different priority numbers than hello ones listed here.</span></span> <span data-ttu-id="a9592-401">Этот список и связанные с ними номера, релевантность tooprovide между только одиннадцать правил и hello относительный приоритет среди них.</span><span class="sxs-lookup"><span data-stu-id="a9592-401">This list and associated numbers are tooprovide relevance between just these eleven rules and hello relative priority amongst them.</span></span> <span data-ttu-id="a9592-402">Другими словами; на брандмауэре фактическое hello hello «TooIIS01 протокола удаленного рабочего СТОЛА» может быть номер правила 5, но пока это под правило «Управление брандмауэром» hello и выше правило «TooDNS01 протокола удаленного рабочего СТОЛА» hello, которое будет соответствовать намерение hello этого списка.</span><span class="sxs-lookup"><span data-stu-id="a9592-402">In other words; on hello actual firewall, hello “RDP tooIIS01” may be rule number 5, but as long as it’s below hello “Firewall Management” rule and above hello “RDP tooDNS01” rule it would align with hello intention of this list.</span></span> <span data-ttu-id="a9592-403">Список Hello поможет hello ниже сценарии, позволяя краткости; Например правило 9 брандмауэра (DNS) (FW Rule 9 (DNS)).</span><span class="sxs-lookup"><span data-stu-id="a9592-403">hello list will also aid in hello below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="a9592-404">Для краткости hello четыре правила протокола удаленного рабочего СТОЛА, будут совместно называется также и «hello правила протокола удаленного рабочего СТОЛА» при несвязанных tooRDP сценарий трафика hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-404">Also for brevity, hello four RDP rules will be collectively called, “hello RDP rules” when hello traffic scenario is unrelated tooRDP.</span></span>

<span data-ttu-id="a9592-405">Также помните, сетевые группы безопасности на месте для входящего трафика Интернета hello переднего плана и подсетей серверной части.</span><span class="sxs-lookup"><span data-stu-id="a9592-405">Also recall that Network Security Groups are in-place for inbound internet traffic on hello Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="a9592-406">(Разрешено) Internet tooWeb Server</span><span class="sxs-lookup"><span data-stu-id="a9592-406">(Allowed) Internet tooWeb Server</span></span>
1. <span data-ttu-id="a9592-407">Интернет-пользователь запрашивает страницу HTTP из службы SecSvc001.CloudApp.Net (облачная служба с выходом в Интернет).</span><span class="sxs-lookup"><span data-stu-id="a9592-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="a9592-408">Облачные службы передает трафик через открытую конечную точку на порт 80 интерфейсе toofirewall 10.0.0.4:80</span><span class="sxs-lookup"><span data-stu-id="a9592-408">Cloud service passes traffic through open endpoint on port 80 toofirewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="a9592-409">Нет NSG назначены подсети tooSecurity, системные правила NSG разрешить трафик toofirewall</span><span class="sxs-lookup"><span data-stu-id="a9592-409">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="a9592-410">Трафик достигнет внутренний IP-адрес брандмауэра hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="a9592-410">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="a9592-411">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="a9592-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="a9592-412">Не применяет правила 1 FW (встроенного по, управление), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-412">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="a9592-413">Правила 2 – 5 (правила RDP) не применяются, переместить toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="a9592-414">FW правила 6 (приложение: Web) применяются, трафик, брандмауэр NAT его too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="a9592-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it too10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="a9592-415">Hello внешней подсети начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="a9592-415">hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="a9592-416">Не применяет правила 1 NSG (Интернету блок) (этот трафик был NAT следует брандмауэром hello, таким образом hello адресом источника теперь является hello брандмауэр, который находится в подсети безопасности hello и видны hello внешней подсети трафика «local» toobe NSG и таким образом может быть), переместить toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Frontend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="a9592-417">По умолчанию правила NSG разрешить подсети toosubnet трафик, трафик, остановите обработки правила NSG</span><span class="sxs-lookup"><span data-stu-id="a9592-417">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="a9592-418">IIS01 прослушивание веб-трафик, получает этот запрос и начинает обработку запроса hello</span><span class="sxs-lookup"><span data-stu-id="a9592-418">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
8. <span data-ttu-id="a9592-419">IIS01 пытается tooinitiates tooAppVM01 сеанс FTP в подсети серверной части</span><span class="sxs-lookup"><span data-stu-id="a9592-419">IIS01 attempts tooinitiates an FTP session tooAppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="a9592-420">маршрут UDR Hello внешней подсети делает hello брандмауэра hello следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="a9592-420">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
10. <span data-ttu-id="a9592-421">В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="a9592-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="a9592-422">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="a9592-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="a9592-423">Не применяет правила 1 FW (встроенного по, управление), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-423">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="a9592-424">Не применять правило FW 2 – 5 (правила протокола удаленного рабочего СТОЛА), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="a9592-425">Правила 6 FW (приложение: Web) не применяются, переместить toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-425">FW Rule 6 (App: Web) doesn’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="a9592-426">Правила 7 FW (приложение: серверной части) применяются, трафик, брандмауэр направляет трафик too10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="a9592-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic too10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="a9592-427">подсети серверной Hello начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="a9592-427">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="a9592-428">Не применяет правила 1 NSG (блок Интернет), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-428">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="a9592-429">По умолчанию правила NSG разрешить подсети toosubnet трафик, трафик, остановите обработки правила NSG</span><span class="sxs-lookup"><span data-stu-id="a9592-429">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="a9592-430">Получает запрос hello и инициирует сеанс hello и отвечает AppVM01</span><span class="sxs-lookup"><span data-stu-id="a9592-430">AppVM01 receives hello request and initiates hello session and responds</span></span>
14. <span data-ttu-id="a9592-431">маршрут UDR Hello в серверной части подсети делает hello брандмауэра hello следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="a9592-431">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
15. <span data-ttu-id="a9592-432">Так как может быть не исходящие правила NSG на hello ответа hello подсети серверной части</span><span class="sxs-lookup"><span data-stu-id="a9592-432">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
16. <span data-ttu-id="a9592-433">Так как это получение трафика на сеанс связи hello пропускает hello ответ назад toohello веб-сервера (IIS01)</span><span class="sxs-lookup"><span data-stu-id="a9592-433">Because this is returning traffic on an established session hello firewall passes hello response back toohello web server (IIS01)</span></span>
17. <span data-ttu-id="a9592-434">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="a9592-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="a9592-435">Не применяет правила 1 NSG (блок Интернет), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-435">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="a9592-436">По умолчанию правила NSG разрешить подсети toosubnet трафик, трафик, остановите обработки правила NSG</span><span class="sxs-lookup"><span data-stu-id="a9592-436">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="a9592-437">сервер IIS Hello получает ответ hello завершает транзакцию hello с AppVM01 и завершает построение hello HTTP-ответа, это HTTP-ответ отправляется запрашивающей стороны toohello</span><span class="sxs-lookup"><span data-stu-id="a9592-437">hello IIS server receives hello response, completes hello transaction with AppVM01, and then completes building hello HTTP response, this HTTP response is sent toohello requestor</span></span>
19. <span data-ttu-id="a9592-438">Так как может быть не исходящие правила NSG на hello интерфейсной подсети hello ответа</span><span class="sxs-lookup"><span data-stu-id="a9592-438">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
20. <span data-ttu-id="a9592-439">Здравствуйте брандмауэра hello попаданий ответа HTTP, а так, как это tooan ответа hello установления сеанса NAT принимается hello брандмауэра</span><span class="sxs-lookup"><span data-stu-id="a9592-439">hello HTTP response hits hello firewall, and because this is hello response tooan established NAT session is accepted by hello firewall</span></span>
21. <span data-ttu-id="a9592-440">брандмауэр Hello выполняет перенаправление назад toohello hello ответа пользователя Интернета</span><span class="sxs-lookup"><span data-stu-id="a9592-440">hello firewall then redirects hello response back toohello Internet User</span></span>
22. <span data-ttu-id="a9592-441">Так как не существует исходящие правила NSG или UDR прыжков на hello внешней подсети разрешено ответа hello и hello пользователя Интернета получает hello веб-страницы, в запросе.</span><span class="sxs-lookup"><span data-stu-id="a9592-441">Since there are no outbound NSG rules or UDR hops on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-internet-rdp-toobackend"></a><span data-ttu-id="a9592-442">(Разрешено) TooBackend Интернет протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="a9592-442">(Allowed) Internet RDP tooBackend</span></span>
1. <span data-ttu-id="a9592-443">Администратор сервера в Интернете запрашивает tooAppVM01 сеанс RDP через SecSvc001.CloudApp.Net:8025, где 8025 — номер порта, пользователь hello правила брандмауэра «RDP tooAppVM01» hello</span><span class="sxs-lookup"><span data-stu-id="a9592-443">Server Admin on internet requests RDP session tooAppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is hello user assigned port number for hello “RDP tooAppVM01” firewall rule</span></span>
2. <span data-ttu-id="a9592-444">Hello облачной службы передает трафик через открытую конечную точку hello на интерфейсе toofirewall 8025 порт 10.0.0.4:8025</span><span class="sxs-lookup"><span data-stu-id="a9592-444">hello cloud service passes traffic through hello open endpoint on port 8025 toofirewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="a9592-445">Нет NSG назначены подсети tooSecurity, системные правила NSG разрешить трафик toofirewall</span><span class="sxs-lookup"><span data-stu-id="a9592-445">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="a9592-446">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="a9592-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="a9592-447">Не применяет правила 1 FW (встроенного по, управление), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-447">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="a9592-448">Не применяется правило 2 FW (RDP IIS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-448">FW Rule 2 (RDP IIS) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="a9592-449">Не применяется правило 3 FW (RDP DNS01), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-449">FW Rule 3 (RDP DNS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="a9592-450">Применить правила 4 FW (RDP AppVM01), трафик, брандмауэр NAT его too10.0.2.5:3386 (RDP-порту на AppVM01)</span><span class="sxs-lookup"><span data-stu-id="a9592-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it too10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="a9592-451">подсети серверной Hello начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="a9592-451">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="a9592-452">Не применяет правила 1 NSG (Интернету блок) (этот трафик был NAT следует брандмауэром hello, таким образом hello адресом источника теперь является hello брандмауэр, который находится в подсети безопасности hello и видны hello серверной подсети трафика «local» toobe NSG и таким образом может быть), переместить toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Backend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="a9592-453">По умолчанию правила NSG разрешить подсети toosubnet трафик, трафик, остановите обработки правила NSG</span><span class="sxs-lookup"><span data-stu-id="a9592-453">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="a9592-454">AppVM01 прослушивает трафик RDP и отвечает.</span><span class="sxs-lookup"><span data-stu-id="a9592-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="a9592-455">Правил для исходящего трафика групп безопасности сети нет, поэтому применяются правила по умолчанию и обратный трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="a9592-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="a9592-456">Брандмауэр toohello UDR маршруты исходящего трафика в качестве следующего прыжка hello</span><span class="sxs-lookup"><span data-stu-id="a9592-456">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
9. <span data-ttu-id="a9592-457">Так как это получение трафика на сеанс связи hello пропускает пользователя Интернета задней toohello ответа hello</span><span class="sxs-lookup"><span data-stu-id="a9592-457">Because this is returning traffic on an established session hello firewall passes hello response back toohello internet user</span></span>
10. <span data-ttu-id="a9592-458">Начинается сеанс RDP.</span><span class="sxs-lookup"><span data-stu-id="a9592-458">RDP session is enabled</span></span>
11. <span data-ttu-id="a9592-459">Сервер AppVM01 запрашивает имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a9592-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="a9592-460">DNS-запрос веб-сервера к серверу DNS (разрешено) </span><span class="sxs-lookup"><span data-stu-id="a9592-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="a9592-461">Веб-сервера, IIS01, потребности в www.data.gov, но потребности tooresolve hello адрес канала данных.</span><span class="sxs-lookup"><span data-stu-id="a9592-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="a9592-462">Hello конфигурацию сети для виртуальной сети hello списков DNS01 (10.0.2.4 подсети hello серверной части) как hello основной DNS-сервер, IIS01 отправляет запрос tooDNS01 hello DNS</span><span class="sxs-lookup"><span data-stu-id="a9592-462">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="a9592-463">Брандмауэр toohello UDR маршруты исходящего трафика в качестве следующего прыжка hello</span><span class="sxs-lookup"><span data-stu-id="a9592-463">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
4. <span data-ttu-id="a9592-464">Нет исходящие правила NSG являются привязанного toohello внешней подсети, трафик</span><span class="sxs-lookup"><span data-stu-id="a9592-464">No outbound NSG rules are bound toohello Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="a9592-465">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="a9592-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="a9592-466">Не применяет правила 1 FW (встроенного по, управление), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-466">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="a9592-467">Не применять правило FW 2 – 5 (правила протокола удаленного рабочего СТОЛА), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="a9592-468">Не применять FW правила 6 и 7 (правила приложений), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-468">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="a9592-469">Не применяется правило FW 8 (tooInternet), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-469">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="a9592-470">Применить правило 9 FW (DNS), трафик, брандмауэр направляет трафик too10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="a9592-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic too10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="a9592-471">подсети серверной Hello начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="a9592-471">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="a9592-472">Не применяет правила 1 NSG (блок Интернет), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-472">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="a9592-473">По умолчанию правила NSG разрешить подсети toosubnet трафик, трафик, остановите обработки правила NSG</span><span class="sxs-lookup"><span data-stu-id="a9592-473">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="a9592-474">DNS-сервер получает запрос hello</span><span class="sxs-lookup"><span data-stu-id="a9592-474">DNS server receives hello request</span></span>
8. <span data-ttu-id="a9592-475">DNS-сервер не имеет адреса hello в кэше и запрашивает у корневой сервер DNS на hello Интернета</span><span class="sxs-lookup"><span data-stu-id="a9592-475">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
9. <span data-ttu-id="a9592-476">Брандмауэр toohello UDR маршруты исходящего трафика в качестве следующего прыжка hello</span><span class="sxs-lookup"><span data-stu-id="a9592-476">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
10. <span data-ttu-id="a9592-477">В подсети Backend нет правил для исходящего трафика групп безопасности сети, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="a9592-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="a9592-478">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="a9592-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="a9592-479">Не применяет правила 1 FW (встроенного по, управление), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-479">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="a9592-480">Не применять правило FW 2 – 5 (правила протокола удаленного рабочего СТОЛА), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="a9592-481">Не применять FW правила 6 и 7 (правила приложений), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-481">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="a9592-482">Применить правило FW 8 (tooInternet), -трафика, сеанс — SNAT out tooroot DNS-сервер в Интернете hello</span><span class="sxs-lookup"><span data-stu-id="a9592-482">FW Rule 8 (tooInternet) does apply, traffic is allowed, session is SNAT out tooroot DNS server on hello Internet</span></span>
12. <span data-ttu-id="a9592-483">Реагирует Internet DNS-сервера, с момента этого сеанса было инициировано из брандмауэра hello, hello ответ принимается hello брандмауэра</span><span class="sxs-lookup"><span data-stu-id="a9592-483">Internet DNS server responds, since this session was initiated from hello firewall, hello response is accepted by hello firewall</span></span>
13. <span data-ttu-id="a9592-484">Как активный сеанс связи, брандмауэр hello направляет запуск сервера DNS01 toohello ответа hello</span><span class="sxs-lookup"><span data-stu-id="a9592-484">As this is an established session, hello firewall forwards hello response toohello initiating server, DNS01</span></span>
14. <span data-ttu-id="a9592-485">подсети серверной Hello начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="a9592-485">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="a9592-486">Не применяет правила 1 NSG (блок Интернет), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-486">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="a9592-487">По умолчанию правила NSG разрешить подсети toosubnet трафик, трафик, остановите обработки правила NSG</span><span class="sxs-lookup"><span data-stu-id="a9592-487">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="a9592-488">Hello DNS-сервер получает и кэширует ответ hello и затем отвечает назад tooIIS01 toohello исходного запроса</span><span class="sxs-lookup"><span data-stu-id="a9592-488">hello DNS server receives and caches hello response, and then responds toohello initial request back tooIIS01</span></span>
16. <span data-ttu-id="a9592-489">маршрут UDR Hello в серверной части подсети делает hello брандмауэра hello следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="a9592-489">hello UDR route on backend subnet makes hello firewall hello next hop</span></span>
17. <span data-ttu-id="a9592-490">Правила NSG не исходящих существует hello серверной подсети, трафик</span><span class="sxs-lookup"><span data-stu-id="a9592-490">No outbound NSG rules exist on hello Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="a9592-491">Это активный сеанс связи на брандмауэре hello, hello ответа перенаправляется сервером IIS задней toohello брандмауэра hello</span><span class="sxs-lookup"><span data-stu-id="a9592-491">This is an established session on hello firewall, hello response is forwarded by hello firewall back toohello IIS server</span></span>
19. <span data-ttu-id="a9592-492">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="a9592-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="a9592-493">Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены</span><span class="sxs-lookup"><span data-stu-id="a9592-493">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="a9592-494">правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello</span><span class="sxs-lookup"><span data-stu-id="a9592-494">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
20. <span data-ttu-id="a9592-495">IIS01 получает hello ответа от DNS01</span><span class="sxs-lookup"><span data-stu-id="a9592-495">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-backend-server-toofrontend-server"></a><span data-ttu-id="a9592-496">(Разрешено) TooFrontend сервера базы данных сервера</span><span class="sxs-lookup"><span data-stu-id="a9592-496">(Allowed) Backend server tooFrontend server</span></span>
1. <span data-ttu-id="a9592-497">Администратор вошел tooAppVM02 по этому Протоколу запросит файл напрямую с сервера IIS01 hello через проводник windows</span><span class="sxs-lookup"><span data-stu-id="a9592-497">An administrator logged on tooAppVM02 via RDP requests a file directly from hello IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="a9592-498">маршрут UDR Hello в серверной части подсети делает hello брандмауэра hello следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="a9592-498">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
3. <span data-ttu-id="a9592-499">Так как может быть не исходящие правила NSG на hello ответа hello подсети серверной части</span><span class="sxs-lookup"><span data-stu-id="a9592-499">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
4. <span data-ttu-id="a9592-500">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="a9592-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="a9592-501">Не применяет правила 1 FW (встроенного по, управление), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-501">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="a9592-502">Не применять правило FW 2 – 5 (правила протокола удаленного рабочего СТОЛА), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="a9592-503">Не применять FW правила 6 и 7 (правила приложений), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-503">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="a9592-504">Не применяется правило FW 8 (tooInternet), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-504">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="a9592-505">Не применяется правило 9 FW (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-505">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="a9592-506">Применить правило FW 10 (внутри подсеть), трафик, брандмауэр передает трафик too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="a9592-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic too10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="a9592-507">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="a9592-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="a9592-508">Не применяет правила 1 NSG (блок Интернет), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-508">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="a9592-509">По умолчанию правила NSG разрешить подсети toosubnet трафик, трафик, остановите обработки правила NSG</span><span class="sxs-lookup"><span data-stu-id="a9592-509">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="a9592-510">При условии, что надлежащую проверку подлинности и авторизации, IIS01 принимает запрос hello и отвечает</span><span class="sxs-lookup"><span data-stu-id="a9592-510">Assuming proper authentication and authorization, IIS01 accepts hello request and responds</span></span>
7. <span data-ttu-id="a9592-511">маршрут UDR Hello внешней подсети делает hello брандмауэра hello следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="a9592-511">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
8. <span data-ttu-id="a9592-512">Так как может быть не исходящие правила NSG на hello интерфейсной подсети hello ответа</span><span class="sxs-lookup"><span data-stu-id="a9592-512">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
9. <span data-ttu-id="a9592-513">Как это существующего сеанса в брандмауэре hello допускается этот ответ и брандмауэра hello возвращает ответ tooAppVM02 hello</span><span class="sxs-lookup"><span data-stu-id="a9592-513">As this is an existing session on hello firewall this response is allowed and hello firewall returns hello response tooAppVM02</span></span>
10. <span data-ttu-id="a9592-514">Подсеть BackEnd начинает обработку правила для входящего трафика:</span><span class="sxs-lookup"><span data-stu-id="a9592-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="a9592-515">Не применяет правила 1 NSG (блок Интернет), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-515">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="a9592-516">По умолчанию правила NSG разрешить подсети toosubnet трафик, трафик, остановите обработки правила NSG</span><span class="sxs-lookup"><span data-stu-id="a9592-516">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="a9592-517">AppVM02 получает ответ hello</span><span class="sxs-lookup"><span data-stu-id="a9592-517">AppVM02 receives hello response</span></span>

#### <a name="denied-internet-direct-tooweb-server"></a><span data-ttu-id="a9592-518">(Запрещено) Прямой tooWeb Internet Server</span><span class="sxs-lookup"><span data-stu-id="a9592-518">(Denied) Internet direct tooWeb Server</span></span>
1. <span data-ttu-id="a9592-519">Пользователь Интернета пытается tooaccess hello веб-сервер, IIS01, через hello FrontEnd001.CloudApp.Net службы</span><span class="sxs-lookup"><span data-stu-id="a9592-519">Internet user tries tooaccess hello web server, IIS01, through hello FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="a9592-520">Поскольку конечные точки не открыты для трафика HTTP, это не будет передан через hello облачной службы и не достигают сервера hello</span><span class="sxs-lookup"><span data-stu-id="a9592-520">Since there are no endpoints open for HTTP traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="a9592-521">Если по некоторым причинам hello конечные точки были открыты, hello NSG (блок Интернет) на внешней подсети hello заблокирует этот трафик</span><span class="sxs-lookup"><span data-stu-id="a9592-521">If hello endpoints were open for some reason, hello NSG (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="a9592-522">И, наконец маршрут UDR hello интерфейсной подсети отправляла весь исходящий трафик от брандмауэра toohello IIS01 как hello следующего прыжка и hello брандмауэра будет видят в этом асимметричного трафика и drop hello исходящего ответа таким образом, по крайней мере три уровня, независимо от защите между hello Интернета и IIS01 через его облачной службы, предотвращая несанкционированный или нарушение прав доступа.</span><span class="sxs-lookup"><span data-stu-id="a9592-522">Finally, hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toobackend-server"></a><span data-ttu-id="a9592-523">(Запрещено) Internet tooBackend Server</span><span class="sxs-lookup"><span data-stu-id="a9592-523">(Denied) Internet tooBackend Server</span></span>
1. <span data-ttu-id="a9592-524">Пользователь Интернета пытается tooaccess файл на AppVM01 через hello BackEnd001.CloudApp.Net службы</span><span class="sxs-lookup"><span data-stu-id="a9592-524">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="a9592-525">Поскольку конечные точки не открыты для общего файлового ресурса, это не будет передан hello облачной службы и не достигают сервера hello</span><span class="sxs-lookup"><span data-stu-id="a9592-525">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="a9592-526">Если по некоторым причинам hello конечные точки были открыты, hello NSG (Интернету блок) заблокирует этот трафик</span><span class="sxs-lookup"><span data-stu-id="a9592-526">If hello endpoints were open for some reason, hello NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="a9592-527">И, наконец маршрут UDR hello отправляла весь исходящий трафик от брандмауэра toohello AppVM01 как hello следующего прыжка и hello брандмауэра будет видят в этом асимметричного трафика и drop hello исходящего ответа таким образом, существует по крайней мере три независимых уровней защиты между Здравствуйте, Интернет и AppVM01 через его облачной службы, предотвращая несанкционированный или нарушение прав доступа.</span><span class="sxs-lookup"><span data-stu-id="a9592-527">Finally, hello UDR route would send any outbound traffic from AppVM01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-toobackend-server"></a><span data-ttu-id="a9592-528">(Запрещено) Сервер переднего плана tooBackend сервера</span><span class="sxs-lookup"><span data-stu-id="a9592-528">(Denied) Frontend server tooBackend Server</span></span>
1. <span data-ttu-id="a9592-529">Предположим, был скомпрометирован IIS01 и выполняется попытка tooscan hello внутренних подсети серверов вредоносный код.</span><span class="sxs-lookup"><span data-stu-id="a9592-529">Assume IIS01 was compromised and is running malicious code trying tooscan hello Backend subnet servers.</span></span>
2. <span data-ttu-id="a9592-530">маршрут UDR Hello интерфейсной подсети отправит весь исходящий трафик от брандмауэра toohello IIS01 как hello следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="a9592-530">hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop.</span></span> <span data-ttu-id="a9592-531">Это не то, что может быть изменено, hello скомпрометированы виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a9592-531">This is not something that can be altered by hello compromised VM.</span></span>
3. <span data-ttu-id="a9592-532">Hello брандмауэра будет обрабатывать трафик hello, если запрос hello был tooAppVM01 или toohello DNS-сервера для DNS-запросы, которые трафика может допускаются потенциально брандмауэра hello (из-за tooFW правила 7 и 9).</span><span class="sxs-lookup"><span data-stu-id="a9592-532">hello firewall would process hello traffic, if hello request was tooAppVM01, or toohello DNS server for DNS lookups that traffic could potentially be allowed by hello firewall (due tooFW Rules 7 and 9).</span></span> <span data-ttu-id="a9592-533">Весь остальной трафик будет заблокирован (запрет любого трафика) правилом 11 брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="a9592-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="a9592-534">Если обнаружение угроз повышенной было включено на брандмауэре hello (которого не рассматривается в этом документе, см. в документации поставщика hello для вашего устройства определенным сетевым расширенными возможностями угроз), даже трафик, который допускается по hello основные правила перенаправления описанные в этом документе может быть не выполняется, если трафик hello содержатся известные подписи или шаблонов, которые флаг правило дополнительные угрозы.</span><span class="sxs-lookup"><span data-stu-id="a9592-534">If advanced threat detection was enabled on hello firewall (which is not covered in this document, see hello vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by hello basic forwarding rules discussed in this document could be prevented if hello traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="a9592-535">DNS-запрос из Интернета к серверу DNS (запрещено)</span><span class="sxs-lookup"><span data-stu-id="a9592-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="a9592-536">Пользователь Интернета пытается toolookup внутренние DNS-запись на DNS01 через службу BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="a9592-536">Internet user tries toolookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="a9592-537">Поскольку конечные точки не открыты для трафика DNS, это не будет передан через hello облачной службы и не достигают сервера hello</span><span class="sxs-lookup"><span data-stu-id="a9592-537">Since there are no endpoints open for DNS traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="a9592-538">Если по некоторым причинам hello конечные точки были открыты, правило NSG hello (блок Интернет) на внешней подсети hello заблокирует этот трафик</span><span class="sxs-lookup"><span data-stu-id="a9592-538">If hello endpoints were open for some reason, hello NSG rule (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="a9592-539">И, наконец подсети UDR hello фоновых маршрутов отправляла весь исходящий трафик от брандмауэра toohello DNS01 как hello следующего прыжка и hello брандмауэра будет видят в этом асимметричного трафика и drop hello исходящего ответа таким образом, по крайней мере три уровня, независимо от защите между hello Интернета и DNS01 через его облачной службы, предотвращая несанкционированный или нарушение прав доступа.</span><span class="sxs-lookup"><span data-stu-id="a9592-539">Finally, hello Backend subnet UDR route would send any outbound traffic from DNS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toosql-access-through-firewall"></a><span data-ttu-id="a9592-540">(Запрещено) TooSQL Интернет-доступ через брандмауэр</span><span class="sxs-lookup"><span data-stu-id="a9592-540">(Denied) Internet tooSQL access through Firewall</span></span>
1. <span data-ttu-id="a9592-541">Интернет-пользователь запрашивает данные SQL из службы SecSvc001.CloudApp.Net (облачная служба с выходом в Интернет).</span><span class="sxs-lookup"><span data-stu-id="a9592-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="a9592-542">Поскольку конечные точки не открыты для SQL, это не будет передан hello облачной службы и не будет достигнут hello брандмауэра</span><span class="sxs-lookup"><span data-stu-id="a9592-542">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="a9592-543">Если конечные точки SQL были открыты для какой-либо причине, брандмауэр hello начинается обработка правил:</span><span class="sxs-lookup"><span data-stu-id="a9592-543">If SQL endpoints were open for some reason, hello firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="a9592-544">Не применяет правила 1 FW (встроенного по, управление), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-544">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="a9592-545">Правила 2 – 5 (правила RDP) не применяются, переместить toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="a9592-546">Не применять правила FW 6 и 7 (правил приложения), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-546">FW Rule 6 & 7 (Application Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="a9592-547">Не применяется правило FW 8 (tooInternet), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-547">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="a9592-548">Не применяется правило 9 FW (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-548">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="a9592-549">Не применяется правило FW 10 (внутри подсеть), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="a9592-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move toonext rule</span></span>
   7. <span data-ttu-id="a9592-550">Правило 11 брандмауэра (запрет любого трафика) применяется — трафик блокируется, дальнейшая обработка правил прекращается.</span><span class="sxs-lookup"><span data-stu-id="a9592-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="a9592-551">Ссылки</span><span class="sxs-lookup"><span data-stu-id="a9592-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="a9592-552">Основной сценарий и конфигурация сети</span><span class="sxs-lookup"><span data-stu-id="a9592-552">Main Script and Network Config</span></span>
<span data-ttu-id="a9592-553">Сохраните hello полный скрипт в файл скрипта PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9592-553">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="a9592-554">Сохраните hello сетевой конфигурации в файл с именем «NetworkConf2.xml».</span><span class="sxs-lookup"><span data-stu-id="a9592-554">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="a9592-555">При необходимости измените hello определенные пользователем переменные.</span><span class="sxs-lookup"><span data-stu-id="a9592-555">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="a9592-556">Запустите сценарий hello, а затем выполните hello брандмауэра правила установки инструкции выше.</span><span class="sxs-lookup"><span data-stu-id="a9592-556">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="a9592-557">Полный сценарий</span><span class="sxs-lookup"><span data-stu-id="a9592-557">Full Script</span></span>
<span data-ttu-id="a9592-558">Этот скрипт будет, на основе hello определяемых пользователем переменных:</span><span class="sxs-lookup"><span data-stu-id="a9592-558">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="a9592-559">Подключение tooan подписки Azure</span><span class="sxs-lookup"><span data-stu-id="a9592-559">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="a9592-560">Создать новую учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="a9592-560">Create a new storage account</span></span>
3. <span data-ttu-id="a9592-561">Создать новую виртуальную сеть и три подсети, как определено в файле конфигурации сети hello</span><span class="sxs-lookup"><span data-stu-id="a9592-561">Create a new VNet and three subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="a9592-562">Соберет пять виртуальных машин: 1 брандмауэр и 4 виртуальных машины с Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a9592-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="a9592-563">Настроит определяемые пользователем маршруты, включая следующее:</span><span class="sxs-lookup"><span data-stu-id="a9592-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="a9592-564">Создание двух новых таблиц маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="a9592-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="a9592-565">Добавление таблиц маршрутов toohello</span><span class="sxs-lookup"><span data-stu-id="a9592-565">Add routes toohello tables</span></span>
   3. <span data-ttu-id="a9592-566">Привязка таблицы tooappropriate подсети</span><span class="sxs-lookup"><span data-stu-id="a9592-566">Bind tables tooappropriate subnets</span></span>
6. <span data-ttu-id="a9592-567">Включить IP-пересылки на приветствия Уязвимости</span><span class="sxs-lookup"><span data-stu-id="a9592-567">Enable IP Forwarding on hello NVA</span></span>
7. <span data-ttu-id="a9592-568">Настроит группу безопасности сети:</span><span class="sxs-lookup"><span data-stu-id="a9592-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="a9592-569">Создаст группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="a9592-569">Creating a NSG</span></span>
   2. <span data-ttu-id="a9592-570">Добавит правило.</span><span class="sxs-lookup"><span data-stu-id="a9592-570">Adding a rule</span></span>
   3. <span data-ttu-id="a9592-571">Привязка hello NSG toohello соответствующие подсети</span><span class="sxs-lookup"><span data-stu-id="a9592-571">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="a9592-572">Этот сценарий PowerShell должен запускаться локально на ПК или сервере, подключенном к Интернету.</span><span class="sxs-lookup"><span data-stu-id="a9592-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9592-573">При запуске этого сценария могут выдаваться предупреждения и другие информационные сообщения PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9592-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="a9592-574">Обращать внимание следует только на сообщения об ошибках, выделенные красным цветом.</span><span class="sxs-lookup"><span data-stu-id="a9592-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="a9592-575">Файл конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="a9592-575">Network Config File</span></span>
<span data-ttu-id="a9592-576">Сохраните этот файл xml с новое местоположение и добавьте ссылку toothis hello файл toohello $NetworkConfigFile переменной в представленном выше сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="a9592-576">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a><span data-ttu-id="a9592-577">Сценарии примера приложения</span><span class="sxs-lookup"><span data-stu-id="a9592-577">Sample Application Scripts</span></span>
<span data-ttu-id="a9592-578">При желании tooinstall образец приложения для этого и других примерах DMZ, оно предоставлено в hello по ссылке: [образец приложения скрипта][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="a9592-578">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Двунаправленная сеть периметра с виртуальным сетевым устройством, группой безопасности сети и определяемыми пользователем маршрутами"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Логическое представление hello правила брандмауэра"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Создание сетевого объекта FrontEnd"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Создание объекта DNS-сервера"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Копия правила RDP по умолчанию"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Правило AppVM01"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Значок перенаправления приложения"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Значок NAT назначения"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Значок передачи"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Правило управления брандмауэром"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Правило RDP брандмауэра"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Правило Интернета брандмауэра"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Правило AppVM01 брандмауэра"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Правило исходящего трафика брандмауэра"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Правило DNS брандмауэра"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Правило брандмауэра для внутреннего трафика виртуальной сети"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Правило запрета брандмауэра"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Активация правила брандмауэра"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
