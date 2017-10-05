---
title: "Пример сети периметра. Создание сети периметра для защиты сетей с брандмауэром, определяемыми пользователем маршрутами и группами безопасности сети | Документация Майкрософт"
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
ms.openlocfilehash: fdb3c5cbd3acee90386352c6f180a71aa81f54fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="example-3--build-a-dmz-to-protect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="b9e6a-103">Пример 3 — защита сетей. Построение сети периметра с брандмауэром, определяемым пользователем маршрутом и группой безопасности сети</span><span class="sxs-lookup"><span data-stu-id="b9e6a-103">Example 3 – Build a DMZ to Protect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="b9e6a-104">[Вернуться на страницу с советами и рекомендациями по построению периметра безопасности][HOME]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="b9e6a-105">В этом примере будет создана сеть периметра (которая называется также DMZ, демилитаризованной зоной, или промежуточной подсетью) с брандмауэром, четырьмя серверами Windows Server, определяемыми пользователем маршрутами, IP-пересылкой и группами безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="b9e6a-106">В нем также будут рассмотрены все используемые команды для более глубокого понимания каждого этапа.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="b9e6a-107">В разделе «Сценарий прохождения трафика» также подробно описано поэтапное прохождение трафика через уровни защиты в сети периметра.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="b9e6a-108">Наконец, в разделе ссылок содержится весь код и приведены инструкции по созданию этой среды для тестирования и экспериментов с различными сценариями.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="b9e6a-109">![Двунаправленная сеть периметра с виртуальным сетевым устройством, группой безопасности сети и определяемыми пользователем маршрутами][1]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="b9e6a-110">Настройка среды</span><span class="sxs-lookup"><span data-stu-id="b9e6a-110">Environment Setup</span></span>
<span data-ttu-id="b9e6a-111">В этом примере используется подписка, которая содержит такие компоненты:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-111">In this example there is a subscription that contains the following:</span></span>

* <span data-ttu-id="b9e6a-112">три облачные службы: SecSvc001, FrontEnd001 и BackEnd001;</span><span class="sxs-lookup"><span data-stu-id="b9e6a-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="b9e6a-113">виртуальная сеть CorpNetwork с тремя подсетями (SecNet, FrontEnd и BackEnd);</span><span class="sxs-lookup"><span data-stu-id="b9e6a-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="b9e6a-114">виртуальное сетевое устройство, которое в этом примере является брандмауэром, подключенным к подсети SecNet;</span><span class="sxs-lookup"><span data-stu-id="b9e6a-114">A network virtual appliance, in this example a firewall, connected to the SecNet subnet</span></span>
* <span data-ttu-id="b9e6a-115">сервер Windows Server, который представляет веб-сервер приложений (IIS01);</span><span class="sxs-lookup"><span data-stu-id="b9e6a-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="b9e6a-116">два сервера Windows Server, представляющих тыловые серверы приложений (AppVM01, AppVM02);</span><span class="sxs-lookup"><span data-stu-id="b9e6a-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="b9e6a-117">сервер Windows Server, который представляет DNS-сервер (DNS01).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="b9e6a-118">В разделе справочной информации приведен сценарий PowerShell, который создает большую часть описанной выше среды.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-118">In the references section below there is a PowerShell script that will build most of the environment described above.</span></span> <span data-ttu-id="b9e6a-119">Сценарий создает также виртуальные машины и сети, но подробного описания этого процесса нет в этом документе.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-119">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span>

<span data-ttu-id="b9e6a-120">Чтобы создать среду, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-120">To build the environment:</span></span>

1. <span data-ttu-id="b9e6a-121">Сохраните XML-файл конфигурации сети, который можно найти в разделе справочной информации (предварительно укажите в файле имена, расположение и IP-адреса в соответствии с нужным сценарием).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-121">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="b9e6a-122">Измените пользовательские переменные в сценарии в соответствии со средой, в которой он будет выполняться (подписки, имена служб и т. д.).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-122">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="b9e6a-123">Запустите сценарий в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-123">Execute the script in PowerShell</span></span>

<span data-ttu-id="b9e6a-124">**Примечание.** Регион, указанный в сценарии PowerShell, должен соответствовать региону, указанному в XML-файле конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-124">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>

<span data-ttu-id="b9e6a-125">После успешного выполнения сценария можно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-125">Once the script runs successfully the following post-script steps may be taken:</span></span>

1. <span data-ttu-id="b9e6a-126">Настройте правила брандмауэра (см. раздел «Описание правил брандмауэра» ниже).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-126">Set up the firewall rules, this is covered in the section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="b9e6a-127">В разделе справочной информации приведены два сценария для настройки веб-сервера и сервера приложений с простым веб-приложением, с помощью которых можно протестировать эту конфигурацию сети периметра.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-127">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="b9e6a-128">После успешного выполнения сценария необходимо выполнить правила брандмауэра. Как это сделать, см. в разделе «Правила брандмауэра».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-128">Once the script runs successfully the firewall rules will need to be completed, this is covered in the section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="b9e6a-129">Определяемые пользователем маршруты</span><span class="sxs-lookup"><span data-stu-id="b9e6a-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="b9e6a-130">По умолчанию следующие системные маршруты определяются так:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-130">By default, the following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="b9e6a-131">VNETLocal всегда является префиксом адресов виртуальной сети для конкретной сети (т. е. он будет изменяться для каждой виртуальной сети в зависимости от способа ее определения).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-131">The VNETLocal is always the defined address prefix(es) of the VNet for that specific network (ie it will change from VNet to VNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="b9e6a-132">Остальные системные маршруты статические и заданы по умолчанию, как указано в таблице выше.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-132">The remaining system routes are static and default as above.</span></span>

<span data-ttu-id="b9e6a-133">Приоритетность определяется так: маршруты обрабатываются с помощью метода совпадения самого длинного префикса (LPM). Так для данного целевого адреса будет использоваться наиболее подходящий маршрут в таблице.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-133">As for priority, routes are processed via the Longest Prefix Match (LPM) method, thus the most specific route in the table would apply to a given destination address.</span></span>

<span data-ttu-id="b9e6a-134">Следовательно, трафик (например, на сервер DNS01, 10.0.2.4), предназначенный для локальной сети (10.0.0.0/16), будет направляться через виртуальную сеть в узел назначения по маршруту 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-134">Therefore, traffic (for example to the DNS01 server, 10.0.2.4) intended for the local network (10.0.0.0/16) would be routed across the VNet to its destination due to the 10.0.0.0/16 route.</span></span> <span data-ttu-id="b9e6a-135">Другими словами, для 10.0.2.4 наиболее подходящим является маршрут 10.0.0.0/16, несмотря на то, что 10.0.0.0/8 и 0.0.0.0/0 также можно применить. Так как эти маршруты подходят меньше, трафик через них не проходит.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-135">In other words, for 10.0.2.4, the 10.0.0.0/16 route is the most specific route, even though the 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="b9e6a-136">Так трафик к 10.0.2.4 проделает следующий прыжок в виртуальной локальной сети и просто направится к узлу назначения.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-136">Thus the traffic to 10.0.2.4 would have a next hop of the local VNet and simply route to the destination.</span></span>

<span data-ttu-id="b9e6a-137">Если трафик предназначен, к примеру, для 10.1.1.1, маршрут 10.0.0.0/16 не будет использоваться, а 10.0.0.0/8 будет наиболее подходящим. Это означает, что трафик будет отброшен (направлен в «черную дыру»), так как следующий прыжок имеет значение Null.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-137">If traffic was intended for 10.1.1.1 for example, the 10.0.0.0/16 route wouldn’t apply, but the 10.0.0.0/8 would be the most specific, and this the traffic would be dropped (“black holed”) since the next hop is Null.</span></span> 

<span data-ttu-id="b9e6a-138">Если узлу назначения не подходят маршруты с префиксами Null или VNETLocal, будет выбран наименее подходящий маршрут 0.0.0.0/0. Тогда трафик следующим прыжком будет направлен в Интернет, таким образом выходя за границы Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-138">If the destination didn’t apply to any of the Null prefixes or the VNETLocal prefixes, then it would follow the least specific route, 0.0.0.0/0 and be routed out to the Internet as the next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="b9e6a-139">При наличии двух одинаковых префиксов в таблице маршрутизации, порядок приоритета определяется на основе атрибута «источник» маршрутов, как приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-139">If there are two identical prefixes in the route table, the following is the order of preference based on the routes “source” attribute:</span></span>

1. <span data-ttu-id="b9e6a-140">VirtualAppliance — определяемый пользователем маршрут, добавленный в таблицу вручную.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-140">"VirtualAppliance" = A User Defined Route manually added to the table</span></span>
2. <span data-ttu-id="b9e6a-141">«VPNGateway» — динамический маршрут (BGP при использовании с гибридными сетями), добавленный динамическим сетевым протоколом. Со временем эти маршруты могут меняться, так как динамический протокол автоматически отражает изменения в одноранговой сети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as the dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="b9e6a-142">«Default» — системные маршруты. Это маршруты виртуальной локальной сети и статические маршруты, как показано в приведенной выше таблице маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-142">“Default” = The System Routes, the local VNet and the static entries as shown in the route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="b9e6a-143">Теперь можно использовать определяемую пользователем маршрутизацию (UDR) с ExpressRoute и VPN-шлюзами, чтобы принудительно перенаправлять распределенный входящий и исходящий трафик на виртуальное сетевое устройство (NVA).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways to force outbound and inbound cross-premises traffic to be routed to a network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-the-local-routes"></a><span data-ttu-id="b9e6a-144">Создание локальных маршрутов</span><span class="sxs-lookup"><span data-stu-id="b9e6a-144">Creating the local routes</span></span>
<span data-ttu-id="b9e6a-145">В этом примере нам понадобится две таблицы маршрутизации: для подсети Frontend и подсети Backend.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-145">In this example, two routing tables are needed, one each for the Frontend and Backend subnets.</span></span> <span data-ttu-id="b9e6a-146">В каждую таблицу загружены статические маршруты для данной подсети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-146">Each table is loaded with static routes appropriate for the given subnet.</span></span> <span data-ttu-id="b9e6a-147">В нашем примере каждая таблица содержит по три маршрута:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-147">For the purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="b9e6a-148">Для трафика локальной подсети значение следующего прыжка не указано, что позволяет трафику локальной подсети обходить брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-148">Local subnet traffic with no Next Hop defined to allow local subnet traffic to bypass the firewall</span></span>
2. <span data-ttu-id="b9e6a-149">Для трафика виртуальной сети значением следующего прыжка установлен адрес брандмауэра. Это значение переопределяет правило по умолчанию, которое разрешает прямое прохождение трафика виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides the default rule that allows local VNet traffic to route directly</span></span>
3. <span data-ttu-id="b9e6a-150">Для всего остального трафика (0/0) значением следующего прыжка задан адрес брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-150">All remaining traffic (0/0) with a Next Hop defined as the firewall</span></span>

<span data-ttu-id="b9e6a-151">После создания таблиц маршрутизации они привязываются к соответствующим подсетям.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-151">Once the routing tables are created they are bound to their subnets.</span></span> <span data-ttu-id="b9e6a-152">После создания и привязки к подсети таблица маршрутизации подсети Frontend будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-152">For the Frontend subnet routing table, once created and bound to the subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="b9e6a-153">В этом примере приведены команды для построения таблицы маршрутизации, добавления определяемого пользователем маршрута и привязки таблицы маршрутизации к подсети. (Обратите внимание, что все указанные ниже элементы со знаком доллара в начале (например, $BESubnet) являются переменными, определяемыми пользователем с помощью скрипта, который содержится в разделе справочной информации этого документа).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-153">For this example, the following commands are used to build the route table, add a user defined route, and then bind the route table to a subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="b9e6a-154">Сначала необходимо создать базовую таблицу маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-154">First the base routing table must be created.</span></span> <span data-ttu-id="b9e6a-155">Приведенный ниже фрагмент кода создает таблицу для подсети Backend.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-155">This snippet shows the creation of the table for the Backend subnet.</span></span> <span data-ttu-id="b9e6a-156">Этот же скрипт создает соответствующую таблицу для подсети Frontend.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-156">In the script, a corresponding table is also created for the Frontend subnet.</span></span>
   
     <span data-ttu-id="b9e6a-157">New-AzureRouteTable -Name $BERouteTableName \`</span><span class="sxs-lookup"><span data-stu-id="b9e6a-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="b9e6a-158">После создания таблицы маршрутизации можно добавить определяемые пользователем маршруты.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-158">Once the route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="b9e6a-159">В этом фрагменте весь трафик (0.0.0.0/0) будет проходить через виртуальное устройство (переменная $VMIP [0] используется для передачи IP-адреса, назначенного при создании виртуального устройства ранее в этом скрипте).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-159">In this snipped, all traffic (0.0.0.0/0) will be routed through the virtual appliance (a variable, $VMIP[0], is used to pass in the IP address assigned when the virtual appliance was created earlier in the script).</span></span> <span data-ttu-id="b9e6a-160">Кроме того, этот скрипт создает соответствующее правило в таблице подсети Frontend.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-160">In the script, a corresponding rule is also created in the Frontend table.</span></span>
   
     <span data-ttu-id="b9e6a-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="b9e6a-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="b9e6a-162">Приведенное выше значение маршрута переопределит маршрут по умолчанию 0.0.0.0/0. Тем не менее правило по умолчанию 10.0.0.0/16 все еще существует и будет разрешать трафику в виртуальной сети направляться непосредственно к назначению, а не к виртуальному сетевому устройству.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-162">The above route entry will override the default "0.0.0.0/0" route, but the default 10.0.0.0/16 rule still existing which would allow traffic within the VNet to route directly to the destination and not to the Network Virtual Appliance.</span></span> <span data-ttu-id="b9e6a-163">Такое поведение можно исправить, добавив необходимое правило.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-163">To correct this behavior the follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="b9e6a-164">На этом этапе вам предстоит сделать выбор.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-164">At this point there is a choice to be made.</span></span> <span data-ttu-id="b9e6a-165">С двумя указанными маршрутами весь трафик будет направляться на брандмауэр для оценки, даже трафик внутри одной подсети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-165">With the above two routes all traffic will route to the firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="b9e6a-166">Это хорошо, но, чтобы разрешить локальную маршрутизацию трафика в подсети без использования брандмауэра, нужно добавить третье, особое правило.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-166">This may be desired, however to allow traffic within a subnet to route locally without involvement from the firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="b9e6a-167">Оно будет указывать, что любой адрес назначения из локальной подсети может направляться напрямую (NextHopType = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-167">This route states that any address destine for the local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="b9e6a-168">И наконец, после создания таблицы маршрутизации и заполнения определяемыми пользователем маршрутами ее нужно привязать к подсети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-168">Finally, with the routing table created and populated with a user defined routes, the table must now be bound to a subnet.</span></span> <span data-ttu-id="b9e6a-169">Кроме того, в скрипте таблица маршрутизации для подсети переднего плана привязана к подсети Frontend.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-169">In the script, the front end route table is also bound to the Frontend subnet.</span></span> <span data-ttu-id="b9e6a-170">Ниже приведен скрипт привязки для внутренней подсети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-170">Here is the binding script for the back end subnet.</span></span>
   
     <span data-ttu-id="b9e6a-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span><span class="sxs-lookup"><span data-stu-id="b9e6a-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="b9e6a-172">IP-пересылку</span><span class="sxs-lookup"><span data-stu-id="b9e6a-172">IP Forwarding</span></span>
<span data-ttu-id="b9e6a-173">Определяемые пользователем маршруты всегда используются вместе с функцией IP-пересылки.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-173">A companion feature to UDR, is IP Forwarding.</span></span> <span data-ttu-id="b9e6a-174">Это параметр для виртуального устройства, который позволяет принимать не адресованный устройству трафик и пересылать его конечному получателю.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-174">This is a setting on a Virtual Appliance that allows it to receive traffic not specifically addressed to the appliance and then forward that traffic to its ultimate destination.</span></span>

<span data-ttu-id="b9e6a-175">Например, если поступает трафик от AppVM01 с запросом к серверу DNS01, определяемый пользователем маршрут направит такой трафик на брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-175">As an example, if traffic from AppVM01 makes a request to the DNS01 server, UDR would route this to the firewall.</span></span> <span data-ttu-id="b9e6a-176">При включенной IP-пересылке трафик с указанным назначением DNS01 (10.0.2.4) будет принят устройством (10.0.0.4) и затем передан конечному получателю (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-176">With IP Forwarding enabled, the traffic for the DNS01 destination (10.0.2.4) will be accepted by the appliance (10.0.0.4) and then forwarded to its ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="b9e6a-177">Если IP-пересылка на брандмауэре не разрешена, такой трафик не будет принят устройством, даже если в качестве следующего прыжка в таблице маршрутизации указан брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-177">Without IP Forwarding enabled on the Firewall, traffic would not be accepted by the appliance even though the route table has the firewall as the next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b9e6a-178">Не забудьте вместе с определяемыми пользователем маршрутами обязательно включить IP-пересылку.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-178">It’s critical to remember to enable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="b9e6a-179">IP-пересылка настраивается с помощью единственной команды. Настройку можно выполнить во время создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="b9e6a-180">В этом примере фрагмент кода находится в конце скрипта и группируется с командами UDR:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-180">For the flow of this example the code snippet is towards the end of the script and grouped with the UDR commands:</span></span>

1. <span data-ttu-id="b9e6a-181">Вызовите экземпляр виртуальной машины, которая является вашим виртуальным устройством и брандмауэром в данном случае, и включите IP-пересылку. Обратите внимание, что все элементы, обозначенные красным, со знаком доллара в начале (например, $VMName[0]) являются переменными, определяемыми пользователем в скрипте, который приведен в разделе справочной информации этого документа.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-181">Call the VM instance that is your virtual appliance, the firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from the script in the reference section of this document.</span></span> <span data-ttu-id="b9e6a-182">Ноль в квадратных скобках, [0], представляет первую виртуальную машину в массиве виртуальных машин. Чтобы пример скрипта работал без изменений, первая виртуальная машина (VM 0) должна быть брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-182">The zero in brackets, [0], represents the first VM in the array of VMs, for the example script to work without modification, the first VM (VM 0) must be the firewall):</span></span>
   
     <span data-ttu-id="b9e6a-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span><span class="sxs-lookup"><span data-stu-id="b9e6a-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="b9e6a-184">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="b9e6a-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="b9e6a-185">В этом примере создается группа безопасности сети, после чего в нее загружается одно правило.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="b9e6a-186">Затем эта группа привязывается только к подсетям Frontend и Backend (не SecNet).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-186">This group is then bound only to the Frontend and Backend subnets (not the SecNet).</span></span> <span data-ttu-id="b9e6a-187">Декларативно создается следующее правило:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-187">Declaratively the following rule is being built:</span></span>

1. <span data-ttu-id="b9e6a-188">Весь трафик (все порты) из Интернета ко всей виртуальной сети (все подсети) запрещается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-188">Any traffic (all ports) from the Internet to the entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="b9e6a-189">В этом примере используются группы безопасности сети, но его основной целью является создание дополнительного уровня защиты от неправильной настройки вручную.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="b9e6a-190">Нам нужно заблокировать весь входящий трафик из Интернета к подсетям Frontend и Backend. Трафик должен проходить только через подсеть SecNet к брандмауэру (а затем — в подсеть Frontend или Backend, при наличии таковых).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-190">We want to block all inbound traffic from the internet to either the Frontend or Backend subnets, traffic should only flow through the SecNet subnet to the firewall (and then if appropriate on to the Frontend or Backend subnets).</span></span> <span data-ttu-id="b9e6a-191">Кроме того, если установлены правила определяемых пользователем маршрутов, любой трафик, поступивший в подсети Frontend и Backend, будет направляться на брандмауэр (благодаря наличию определяемых пользователем маршрутов).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-191">Plus, with the UDR rules in place, any traffic that did make it into the Frontend or Backend subnets would be directed out to the firewall (thanks to UDR).</span></span> <span data-ttu-id="b9e6a-192">Брандмауэр воспримет это как асимметричный поток и отбросит исходящий трафик.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-192">The firewall would see this as an asymmetric flow and would drop the outbound traffic.</span></span> <span data-ttu-id="b9e6a-193">Следовательно, существует три уровня безопасности для защиты подсетей Frontend и Backend: 1) отсутствие открытых конечных точек в облачных службах FrontEnd001 и BackEnd001, 2) группы безопасности сети, запрещающие трафик из Интернета, 3) брандмауэр, отбрасывающий асимметричный трафик.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-193">Thus there are three layers of security protecting the Frontend and Backend subnets; 1) no open endpoints on the FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from the Internet, 3) the firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="b9e6a-194">В приведенном ниже примере есть интересная особенность, касающаяся сетевой группы безопасности. В нем содержится только одно правило (указанное ниже), которое запрещает Интернет-трафик ко всей виртуальной сети, включая подсеть безопасности.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-194">One interesting point regarding the Network Security Group in this example is that it contains only one rule, shown below, which is to deny internet traffic to the entire virtual network which would include the Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet `
        from the Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="b9e6a-195">Однако, так как сетевая группа безопасности привязана только к подсети переднего плана и внутренней подсети, это правило не применяется к входящему трафику подсети безопасности.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-195">However, since the NSG is only bound to the Frontend and Backend subnets, the rule isn’t processed on traffic inbound to the Security subnet.</span></span> <span data-ttu-id="b9e6a-196">В результате трафик будет попадать в подсеть безопасности, поскольку правило сетевой группы безопасности, запрещающее интернет-трафик на любой адрес виртуальной сети, не было привязано к подсети безопасности.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-196">As a result, even though the NSG rule says no Internet traffic to any address on the VNet, because the NSG was never bound to the Security subnet, traffic will flow to the Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="b9e6a-197">Правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="b9e6a-197">Firewall Rules</span></span>
<span data-ttu-id="b9e6a-198">В брандмауэре необходимо создать правила пересылки.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-198">On the firewall, forwarding rules will need to be created.</span></span> <span data-ttu-id="b9e6a-199">Так как брандмауэр блокирует или пересылает весь входящий, исходящий и внутренний трафик виртуальной сети, требуется много правил брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-199">Since the firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="b9e6a-200">Кроме того, весь входящий трафик будет попадать на общедоступный IP-адрес службы безопасности (на разных портах) для последующей обработки брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-200">Also, all inbound traffic will hit the Security Service public IP address (on different ports), to be processed by the firewall.</span></span> <span data-ttu-id="b9e6a-201">Прежде чем настраивать подсети и правила брандмауэра, рекомендуем составить схему логических потоков, чтобы избежать переделывания позже.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-201">A best practice is to diagram the logical flows before setting up the subnets and firewall rules to avoid rework later.</span></span> <span data-ttu-id="b9e6a-202">Следующий рисунок является логическим представлением правил брандмауэра для этого примера.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-202">The following figure is a logical view of the firewall rules for this example:</span></span>

<span data-ttu-id="b9e6a-203">![Логическое представление правил брандмауэра][2]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-203">![Logical View of the Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="b9e6a-204">Порты управления будут различными в зависимости от используемого виртуального сетевого устройства.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-204">Based on the Network Virtual Appliance used, the management ports will vary.</span></span> <span data-ttu-id="b9e6a-205">В этом примере брандмауэр Barracuda NextGen Firewall использует порты 22, 801 и 807.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="b9e6a-206">Обратитесь к документации поставщика устройства, чтобы точно знать, какие порты используются для управления устройством.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-206">Please consult the appliance vendor documentation to find the exact ports used for management of the device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="b9e6a-207">Описание логического правила</span><span class="sxs-lookup"><span data-stu-id="b9e6a-207">Logical Rule Description</span></span>
<span data-ttu-id="b9e6a-208">На приведенной выше логической схеме не отображена подсеть безопасности, так как брандмауэр является единственным ресурсом в этой подсети. Кроме того, вместо фактического пути маршрутизации на схеме показаны правила брандмауэра и логика разрешения или запрета трафика.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-208">In the logical diagram above, the security subnet is not shown since the firewall is the only resource on that subnet, and this diagram is showing the firewall rules and how they logically allow or deny traffic flows and not the actual routed path.</span></span> <span data-ttu-id="b9e6a-209">Кроме того, внешние порты, выбранные для трафика RDP, являются портами высшего диапазона (8014–8026) и выбраны для совмещения с последними двумя октетами локального IP-адреса для облегчения чтения (например, адрес локального сервера 10.0.1.4 связан с внешним портом 8014). Тем не менее можно использовать любые неконфликтующие порты высшего диапазона.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-209">Also, the external ports selected for the RDP traffic are higher ranged ports (8014 – 8026) and were selected to somewhat align with the last two octets of the local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="b9e6a-210">В этом примере нам нужно 7 типов правил. Их описание приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="b9e6a-211">Внешние правила (для входящего трафика):</span><span class="sxs-lookup"><span data-stu-id="b9e6a-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="b9e6a-212">Правило управления брандмауэром. Это правило перенаправления приложения разрешает пересылать трафик на порты управления виртуального сетевого устройства.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-212">Firewall Management Rule: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance.</span></span>
  2. <span data-ttu-id="b9e6a-213">Правила RDP (для каждого сервера Windows Server). Эти четыре правила (по одному для каждого сервера) позволяют управлять серверами через RDP.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of the individual servers via RDP.</span></span> <span data-ttu-id="b9e6a-214">Эти правила можно объединить в одно, если виртуальное сетевое устройство поддерживает такую возможность.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-214">This could also be bundled into one rule depending on the capabilities of the Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="b9e6a-215">Правила трафика приложений. Существует два правила трафика приложений: первое — для веб-трафика подсети переднего плана, а второе — для трафика внутренней подсети (например, от веб-сервера к уровню данных).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-215">Application Traffic Rules: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span></span> <span data-ttu-id="b9e6a-216">Параметры этих правил будут зависеть от архитектуры сети размещения серверов и характеристик потоков трафика (направление потока и используемые порты).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-216">The configuration of these rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="b9e6a-217">Первое правило позволяет фактическому трафику приложения достигать сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-217">The first rule will allow the actual application traffic to reach the application server.</span></span> <span data-ttu-id="b9e6a-218">Другие правила нужны для безопасности, управления и т. д., а правила приложений позволяют внешним пользователям и службам взаимодействовать с приложениями.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-218">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span></span> <span data-ttu-id="b9e6a-219">В этом примере используется один веб-сервер на порту 80, поэтому на брандмауэре потребуется одно правило приложения. Оно принимает трафик, поступающий на внешний IP-адрес, и переправляет его на внутренний IP-адрес веб-серверов.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span></span> <span data-ttu-id="b9e6a-220">Затем этот трафик обрабатывается службой NAT (преобразование сетевых адресов) и передается на внутренний сервер.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-220">The redirected traffic session would be NAT’d to the internal server.</span></span>
     * <span data-ttu-id="b9e6a-221">Второе правило трафика приложения используется для внутренней подсети. Оно разрешает веб-серверу обращаться к серверу AppVM01 (но не AppVM02) через любой порт.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-221">The second Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="b9e6a-222">Внутренние правила (для внутреннего трафика виртуальной сети)</span><span class="sxs-lookup"><span data-stu-id="b9e6a-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="b9e6a-223">Правило трафика, исходящего в Интернет. Это правило разрешает передачу трафика из любой сети в указанные сети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-223">Outbound to Internet Rule: This rule will allow traffic from any network to pass to the selected networks.</span></span> <span data-ttu-id="b9e6a-224">Обычно это правило является заданным в брандмауэре по умолчанию и при этом отключенным.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-224">This rule is usually a default rule already on the firewall, but in a disabled state.</span></span> <span data-ttu-id="b9e6a-225">В нашем примере это правило следует активировать.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="b9e6a-226">Правило DNS. Это правило разрешает передавать на DNS-сервер только трафик DNS (на порт 53).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-226">DNS Rule: This rule allows only DNS (port 53) traffic to pass to the DNS server.</span></span> <span data-ttu-id="b9e6a-227">Для этой среды блокируется почти весь трафик от подсети Frontend к Backend, а это правило отдельно разрешает трафик DNS из любой локальной подсети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-227">For this environment most traffic from the Frontend to the Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="b9e6a-228">Правило трафика между подсетями. Это правило позволяет любому серверу внутренней подсети подключаться к любому серверу в подсети переднего плана (но не наоборот).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-228">Subnet to Subnet Rule: This rule is to allow any server on the back end subnet to connect to any server on the front end subnet (but not the reverse).</span></span>
* <span data-ttu-id="b9e6a-229">Резервное правило (для трафика, который не соответствует указанным выше правилам).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-229">Fail-safe Rule (for traffic that doesn’t meet any of the above):</span></span>
  1. <span data-ttu-id="b9e6a-230">Правило запрета любого трафика. Это правило всегда должно быть последним (по приоритету). Если трафик не соответствует ни одному из предыдущих правил, этим правилом он будет отброшен.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-230">Deny All Traffic Rule: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="b9e6a-231">Это правило обычно уже установлено по умолчанию и активировано, поэтому не требует дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="b9e6a-232">Второе правило трафика приложения разрешает трафик на любой порт (для упрощения примера). В реальной системе следует использовать как можно более узкие диапазоны портов и адресов, чтобы снизить площадь поражения от атак, обусловленных применением этого правила.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-232">On the second application traffic rule, any port is allowed for easy of this example, in a real scenario the most specific port and address ranges should be used to reduce the attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="b9e6a-233">После создания всех приведенных выше правил обязательно проверьте приоритет каждого правила, чтобы разрешения и запреты трафика выполнялись надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-233">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="b9e6a-234">В нашем примере правила расположены в порядке приоритета.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-234">For this example, the rules are in priority order.</span></span> <span data-ttu-id="b9e6a-235">Очень просто заблокировать брандмауэр из-за неправильного порядка правил.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-235">It's easy to be locked out of the firewall due to mis-ordered rules.</span></span> <span data-ttu-id="b9e6a-236">Поэтому следите за тем, чтобы управление брандмауэром всегда было правилом наивысшего приоритета.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-236">At a minimum, ensure the management for the firewall itself is always the absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="b9e6a-237">Предварительные требования для правил</span><span class="sxs-lookup"><span data-stu-id="b9e6a-237">Rule Prerequisites</span></span>
<span data-ttu-id="b9e6a-238">Предварительным требованием для виртуальной машины, на которой включен брандмауэр, являются общедоступные конечные точки.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-238">One prerequisite for the Virtual Machine running the firewall are public endpoints.</span></span> <span data-ttu-id="b9e6a-239">Чтобы брандмауэр мог обрабатывать трафик, соответствующие общедоступные конечные точки должны быть открыты.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-239">For the firewall to process traffic the appropriate public endpoints must be open.</span></span> <span data-ttu-id="b9e6a-240">В этом примере используется три типа трафика: 1) трафик управления брандмауэром и правилами брандмауэра, 2) трафик RDP для управления серверами Windows Server и 3) трафик приложения.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-240">There are three types of traffic in this example; 1) Management traffic to control the firewall and firewall rules, 2) RDP traffic to control the windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="b9e6a-241">Эти типы трафика представлены в виде трех колонок в верхней части логического представления правил брандмауэра, которое приведено выше.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-241">These are the three columns of traffic types in the upper half of logical view of the firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9e6a-242">Основное, что следует запомнить: **весь** трафик будет проходить через брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-242">A key takeway here is to remember that **all** traffic will come through the firewall.</span></span> <span data-ttu-id="b9e6a-243">Так, для подключения к удаленному рабочему столу сервера IIS01, даже если он находится в облачной службе Front End, и, соответственно, для доступа к подсети Front End необходимо подключиться с помощью RDP к порту 8014 брандмауэра, а затем разрешить брандмауэру отправить запрос RDP внутри сети на порт RDP IIS01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-243">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span></span> <span data-ttu-id="b9e6a-244">Кнопка «Подключиться» на портале Azure не будет работать из-за отсутствия прямого пути RDP к IIS01 (с точки зрения портала).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-244">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span></span> <span data-ttu-id="b9e6a-245">Это означает, что все подключения из Интернета будут поступать в службу безопасности и на порт, например secscv001.cloudapp.net:xxxx (см. схему выше для сопоставления внешних портов и внутренних IP-адресов и портов).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-245">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference the above diagram for the mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="b9e6a-246">Конечную точку можно открыть во время создания виртуальной машины или после сборки, как показано ниже в примере скрипта в этом фрагменте кода. (Обратите внимание, что все элементы со знаком доллара в начале (например, $VMName[$i]) являются переменными, определяемыми пользователем в скрипте, который приведен в разделе справочной информации этого документа.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-246">An endpoint can be opened either at the time of VM creation or post build as is done in the example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from the script in the reference section of this document.</span></span> <span data-ttu-id="b9e6a-247">«$I» в квадратных скобках, [$i], является номером массива определенной виртуальной машины в массиве виртуальных машин.)</span><span class="sxs-lookup"><span data-stu-id="b9e6a-247">The “$i” in brackets, [$i], represents the array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="b9e6a-248">Конечные точки открываются **только** в облачной службе безопасности, хотя здесь это не показано явно из-за использования переменных.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-248">Although not clearly shown here due to the use of variables, but endpoints are **only** opened on the Security Cloud Service.</span></span> <span data-ttu-id="b9e6a-249">Это гарантирует, что весь входящий трафик будет обрабатываться (маршрутизироваться, транслироваться с помощью NAT или отбрасываться) брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-249">This is to ensure that all inbound traffic is handled (routed, NAT'd, dropped) by the firewall.</span></span>

<span data-ttu-id="b9e6a-250">Для управления брандмауэром и создания необходимых конфигураций на компьютер необходимо установить клиент управления.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-250">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span></span> <span data-ttu-id="b9e6a-251">Инструкции по управлению устройством см. в документации брандмауэра (или другого виртуального сетевого устройства).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-251">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span></span> <span data-ttu-id="b9e6a-252">В оставшейся части этого раздела и следующем разделе «Создание правил брандмауэра» описывается конфигурация брандмауэра с помощью клиента управления поставщика (т. е. без использования портала Azure или PowerShell).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-252">The remainder of this section and the next section, Firewall Rules Creation, will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span></span>

<span data-ttu-id="b9e6a-253">Инструкции по загрузке клиента и подключению к брандмауэру Barracuda, который используется в этом примере, см в статье [Администрирование Barracuda NG](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="b9e6a-253">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="b9e6a-254">После входа в брандмауэр можно упростить процесс создания правил с помощью двух предварительно созданных классов объектов — сетевых и служебных (но делать это нужно до создания правил).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-254">Once logged onto the firewall but before creating firewall rules, there are two prerequisite object classes that can make creating the rules easier; Network & Service objects.</span></span>

<span data-ttu-id="b9e6a-255">В этом примере нам нужно определить три именованных сетевых объекта (по одному для подсетей Frontend и Backend, а также сетевой объект для IP-адреса DNS-сервера).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-255">For this example, three named network objects should be defined (one for the Frontend subnet and the Backend subnet, also a network object for the IP address of the DNS server).</span></span> <span data-ttu-id="b9e6a-256">Чтобы создать именованную сеть, откройте панель мониторинга администратора Barracuda NG, перейдите на вкладку «Конфигурация», в разделе «Рабочая конфигурация» щелкните пункт «Набор правил», затем в меню «Объекты брандмауэра» выберите «Сети» и щелкните «Создать» в меню «Изменение сетей».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-256">To create a named network; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Networks” under the Firewall Objects menu, then click New in the Edit Networks menu.</span></span> <span data-ttu-id="b9e6a-257">Теперь можно создать сетевой объект, добавив имя и префикс.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-257">The network object can now be created, by adding the name and the prefix:</span></span>

<span data-ttu-id="b9e6a-258">![Создание сетевого объекта FrontEnd][3]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="b9e6a-259">В результате будет создана именованная сеть для подсети FrontEnd. Для подсети BackEnd следует создать такой же объект.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-259">This will create a named network for the FrontEnd subnet, a similar object should be created for the BackEnd subnet as well.</span></span> <span data-ttu-id="b9e6a-260">Теперь, когда у подсетей есть имена, их проще использовать в правилах брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-260">Now the subnets can be more easily referenced by name in the firewall rules.</span></span>

<span data-ttu-id="b9e6a-261">Для объекта «DNS-сервер»:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-261">For the DNS Server Object:</span></span>

<span data-ttu-id="b9e6a-262">![Создание объекта сервера DNS][4]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="b9e6a-263">Мы будем ссылаться на этот IP-адрес в правиле DNS позднее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-263">This single IP address reference will be utilized in a DNS rule later in the document.</span></span>

<span data-ttu-id="b9e6a-264">Вторым предварительным требованием является наличие служебных объектов.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-264">The second prerequisite objects are Services objects.</span></span> <span data-ttu-id="b9e6a-265">Они будут представлять порты подключения RDP для каждого сервера.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-265">These will represent the RDP connection ports for each server.</span></span> <span data-ttu-id="b9e6a-266">Так как существующий служебный объект RDP привязан к порту RDP по умолчанию 3389, можно создать новые службы для разрешения трафика от внешних портов (8014–8026).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-266">Since the existing RDP service object is bound to the default RDP port, 3389, new Services can be created to allow traffic from the external ports (8014-8026).</span></span> <span data-ttu-id="b9e6a-267">Кроме того, в существующую службу RDP можно добавить новые порты, но для удобства демонстрации создадим для каждого сервера отдельное правило.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-267">The new ports could also be added to the existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="b9e6a-268">Чтобы создать новое правило RDP, откройте панель мониторинга администратора Barracuda NG, перейдите на вкладку «Конфигурация», в разделе «Рабочая конфигурация» щелкните пункт «Набор правил» и в меню «Объекты брандмауэра» выберите «Службы», затем прокрутите список служб вниз и выберите службу RDP.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-268">To create a new RDP rule for a server; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Services” under the Firewall Objects menu, scroll down the list of services and select the “RDP” service.</span></span> <span data-ttu-id="b9e6a-269">Щелкните правой кнопкой мыши и выберите копию, затем щелкните правой кнопкой мыши и выберите команду «Вставить».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="b9e6a-270">Теперь у нас есть объект службы RDP-Copy1, который можно редактировать.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="b9e6a-271">Щелкните правой кнопкой мыши RDP-Copy1 и выберите «Изменить». После этого отобразится окно «Изменение объекта службы», приведенное ниже.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-271">Right-click RDP-Copy1 and select Edit, the Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="b9e6a-272">![Копия правила RDP по умолчанию][5]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="b9e6a-273">Значения можно будет изменять для представления службы RDP определенному серверу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-273">The values can then be edited to represent the RDP service for a specific server.</span></span> <span data-ttu-id="b9e6a-274">Для AppVM01 указанное выше правило RDP по умолчанию необходимо отредактировать в соответствии с новым именем службы, описанием и внешним портом RDP, который используется в схеме на рисунке 8. (Обратите внимание, что порт RDP по умолчанию 3389 меняется на внешний порт, используемый для этого сервера. В случае AppVM01 таковым является внешний порт 8025.) Измененная служба приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-274">For AppVM01 the above default RDP rule should be modified to reflect a new Service Name, Description, and external RDP Port used in the Figure 8 diagram (Note: the ports are changed from the RDP default of 3389 to the external port being used for this specific server, in the case of AppVM01 the external Port is 8025) the modified service is shown below:</span></span>

<span data-ttu-id="b9e6a-275">![Правило AppVM01][6]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="b9e6a-276">Повторите этот процесс для создания служб RDP для остальных серверов: AppVM02, DNS01 и IIS01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-276">This process must be repeated to create RDP Services for the remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="b9e6a-277">После создания этих служб создавать правила станет проще. Вы убедитесь в этом в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-277">The creation of these Services will make the Rule creation simpler and more obvious in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="b9e6a-278">Служба RDP не нужна для брандмауэра по двум причинам: во-первых, брандмауэр является виртуальной машиной на основе Linux, поэтому для управления им будет использоваться SSH на порте 22, а не RDP; во-вторых, порт 22 и два других порта управления разрешены в первом правиле управления, описанном ниже, для управления подключением.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-278">An RDP service for the Firewall is not needed for two reasons; 1) first the firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in the first management rule described below to allow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="b9e6a-279">Создание правил брандмауэра</span><span class="sxs-lookup"><span data-stu-id="b9e6a-279">Firewall Rules Creation</span></span>
<span data-ttu-id="b9e6a-280">В этом примере используется три типа правил брандмауэра. Все они имеют собственные значки.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="b9e6a-281">Правило перенаправления приложения: ![Значок перенаправления приложения][7]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-281">The Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="b9e6a-282">Правило NAT назначения: ![Значок NAT назначения][8]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-282">The Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="b9e6a-283">Разрешающее правило: ![Значок передачи][9]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-283">The Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="b9e6a-284">Дополнительные сведения об этих правилах можно найти на веб-сайте Barracuda.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-284">More information on these rules can be found at the Barracuda web site.</span></span>

<span data-ttu-id="b9e6a-285">Создать следующие правила (или проверить существующие правила по умолчанию) можно так: откройте панель мониторинга администратора Barracuda NG, перейдите на вкладку «Конфигурация» и в разделе «Рабочая конфигурация» щелкните «Набор правил».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-285">To create the following rules (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="b9e6a-286">Откроется сетка «Основные правила», на которой будут отображаться существующие активные и неактивные правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-286">A grid called, “Main Rules” will show the existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="b9e6a-287">В правом верхнем углу этой сетки расположена небольшая зеленая кнопка «+». Нажмите ее, чтобы создать новое правило. (Примечание. Брандмауэр может быть «заблокирован» для внесения изменений. Если вы видите кнопку «Заблокировано» и не можете создать или изменить правила, нажмите эту кнопку, чтобы «разблокировать» набор правил и разрешить редактирование.)</span><span class="sxs-lookup"><span data-stu-id="b9e6a-287">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the rule set and allow editing).</span></span> <span data-ttu-id="b9e6a-288">Если вы хотите изменить существующее правило, выберите его, щелкните правой кнопкой мыши и выберите «Изменить правило».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-288">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="b9e6a-289">После создания или изменения правила необходимо отправить в брандмауэр и затем активировать. Без этого правило не будет действовать.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-289">Once your rules are created and/or modified, they must be pushed to the firewall and then activated, if this is not done the rule changes will not take effect.</span></span> <span data-ttu-id="b9e6a-290">Процесс отправки и активации приведен после описания правил.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-290">The push and activation process is described below the details rule descriptions.</span></span>

<span data-ttu-id="b9e6a-291">Ниже описаны особенности правил, которые используются в нашем примере.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-291">The specifics of each rule required to complete this example are described as follows:</span></span>

* <span data-ttu-id="b9e6a-292">**Правило управления брандмауэром.** Это правило перенаправления приложения разрешает пересылать трафик на порты управления виртуального сетевого устройства (в нашем примере это брандмауэр Barracuda NextGen Firewall).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-292">**Firewall Management Rule**: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="b9e6a-293">Портами управления являются 801, 807 и, при необходимости, порт 22.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-293">The management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="b9e6a-294">Внешние и внутренние порты совпадают (т. е. преобразование портов не используется).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-294">The external and internal ports are the same (i.e. no port translation).</span></span> <span data-ttu-id="b9e6a-295">SETUP-MGMT-ACCESS является правилом по умолчанию и включено по умолчанию (в брандмауэре Barracuda NextGen Firewall версии 6.1).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="b9e6a-296">![Правило управления брандмауэром][10]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="b9e6a-297">Адресное пространство источника в этом правиле — Any, если известны диапазоны IP-адресов управления. Сократите диапазоны, чтобы уменьшить возможность атак на портах управления.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-297">The source address space in this rule is Any, if the management IP address ranges are known, reducing this scope would also reduce the attack surface to the management ports.</span></span>
> 
> 

* <span data-ttu-id="b9e6a-298">**Правила RDP.** Эти правила NAT назначения будут разрешать управление отдельными серверами по протоколу RDP.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-298">**RDP Rules**:  These Destination NAT rules will allow management of the individual servers via RDP.</span></span>
  <span data-ttu-id="b9e6a-299">Создание этого правила предусматривает заполнение четырех важных полей.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-299">There are four critical fields needed to create this rule:</span></span>
  
  1. <span data-ttu-id="b9e6a-300">Источник: чтобы разрешать RDP из любого места, в поле источника необходимо установить значение «Any».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-300">Source – to allow RDP from anywhere, the reference “Any” is used in the Source field.</span></span>
  2. <span data-ttu-id="b9e6a-301">Служба: используйте соответствующий объект службы, созданный ранее, в данном случае — AppVM01 RDP. Трафик, который поступает на внешние порты, перенаправляется на локальный IP-адрес сервера и порт 3389 (порт RDP по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-301">Service – use the appropriate Service Object created earlier, in this case “AppVM01 RDP”, the external ports redirect to the servers local IP address and to port 3386 (the default RDP port).</span></span> <span data-ttu-id="b9e6a-302">Это правило предназначено для доступа к AppVM01 по протоколу RDP.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-302">This specific rule is for RDP access to AppVM01.</span></span>
  3. <span data-ttu-id="b9e6a-303">"Назначение". В этом поле следует указать *локальный порт на брандмауэре*, а именно DCHP 1 Local IP или eth0 при использовании статических IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-303">Destination – should be the *local port on the firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="b9e6a-304">Порядковый номер (eth0, eth1, и т. д.) может отличаться, если сетевое устройство имеет несколько локальных интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-304">The ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="b9e6a-305">Это порт, из которого брандмауэр отправляет трафик (может быть таким же, как принимающий порт). Фактическое назначение указано в поле «Целевой список».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-305">This is the port the firewall is sending out from (may be the same as the receiving port), the actual routed destination is in the Target List field.</span></span>
  4. <span data-ttu-id="b9e6a-306">Перенаправление: в этом разделе указано назначение, в которое виртуальное устройство должно в конечном счете перенаправить трафик.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-306">Redirection – this section tells the virtual appliance where to ultimately redirect this traffic.</span></span> <span data-ttu-id="b9e6a-307">Примером самого простого перенаправления может быть задание IP-адреса и порта (необязательно) в поле «Целевой список».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-307">The simplest redirection is to place the IP and Port (optional) in the Target List field.</span></span> <span data-ttu-id="b9e6a-308">Если порт не указан, для входящего запроса будет использоваться порт назначения (т. е. без трансляции). Если порт указан, он будет транслирован с помощью NAT вместе с IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-308">If no port is used the destination port on the inbound request will be used (ie no translation), if a port is designated the port will also be NAT’d along with the IP address.</span></span>
     
     <span data-ttu-id="b9e6a-309">![Правило RDP брандмауэра][11]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="b9e6a-310">Необходимо создать четыре правила RDP:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-310">A total of four RDP rules will need to be created:</span></span> 
     
     | <span data-ttu-id="b9e6a-311">Имя правила</span><span class="sxs-lookup"><span data-stu-id="b9e6a-311">Rule Name</span></span> | <span data-ttu-id="b9e6a-312">сервер;</span><span class="sxs-lookup"><span data-stu-id="b9e6a-312">Server</span></span> | <span data-ttu-id="b9e6a-313">служба</span><span class="sxs-lookup"><span data-stu-id="b9e6a-313">Service</span></span> | <span data-ttu-id="b9e6a-314">Целевой список</span><span class="sxs-lookup"><span data-stu-id="b9e6a-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="b9e6a-315">RDP-to-IIS01</span><span class="sxs-lookup"><span data-stu-id="b9e6a-315">RDP-to-IIS01</span></span> |<span data-ttu-id="b9e6a-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="b9e6a-316">IIS01</span></span> |<span data-ttu-id="b9e6a-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="b9e6a-317">IIS01 RDP</span></span> |<span data-ttu-id="b9e6a-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="b9e6a-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="b9e6a-319">RDP-to-DNS01</span><span class="sxs-lookup"><span data-stu-id="b9e6a-319">RDP-to-DNS01</span></span> |<span data-ttu-id="b9e6a-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="b9e6a-320">DNS01</span></span> |<span data-ttu-id="b9e6a-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="b9e6a-321">DNS01 RDP</span></span> |<span data-ttu-id="b9e6a-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="b9e6a-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="b9e6a-323">RDP-to-AppVM01</span><span class="sxs-lookup"><span data-stu-id="b9e6a-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="b9e6a-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="b9e6a-324">AppVM01</span></span> |<span data-ttu-id="b9e6a-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="b9e6a-325">AppVM01 RDP</span></span> |<span data-ttu-id="b9e6a-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="b9e6a-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="b9e6a-327">RDP-to-AppVM02</span><span class="sxs-lookup"><span data-stu-id="b9e6a-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="b9e6a-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="b9e6a-328">AppVM02</span></span> |<span data-ttu-id="b9e6a-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="b9e6a-329">AppVm02 RDP</span></span> |<span data-ttu-id="b9e6a-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="b9e6a-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="b9e6a-331">Сужение диапазонов в полях «Источник» и «Служба» позволит снизить возможность атак.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-331">Narrowing down the scope of the Source and Service fields will reduce the attack surface.</span></span> <span data-ttu-id="b9e6a-332">Следует использовать диапазоны как можно уже, которые будут обеспечивать лишь необходимую функциональность.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-332">The most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="b9e6a-333">**Правила трафика приложений.** Доступно два правила трафика приложений: первое — для веб-трафика подсети переднего плана, а второе — для трафика внутренней подсети (например, от веб-сервера к уровню данных).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-333">**Application Traffic Rules**: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span></span> <span data-ttu-id="b9e6a-334">Эти правила зависят от архитектуры сети (размещения серверов) и потоков трафика (их направления и используемых портов).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-334">These rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="b9e6a-335">Сначала рассмотрим правило веб-трафика в подсети переднего плана.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-335">First discussed is the front end rule for web traffic:</span></span>
  
    <span data-ttu-id="b9e6a-336">![Веб-правило брандмауэра][12]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="b9e6a-337">Правило NAT назначения позволяет фактическому трафику приложения получать доступ к серверу приложений.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-337">This Destination NAT rule allows the actual application traffic to reach the application server.</span></span> <span data-ttu-id="b9e6a-338">Другие правила нужны для безопасности, управления и т. д., а правила приложений позволяют внешним пользователям и службам взаимодействовать с приложениями.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-338">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span></span> <span data-ttu-id="b9e6a-339">В этом примере используется один веб-сервер на порте 80. Соответственно, одно правило приложения брандмауэра будет перенаправлять входящий трафик на внешний IP-адрес, на внутренний IP-адрес веб-серверов.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-339">For this example, there is a single web server on port 80, thus the single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span></span>
  
    <span data-ttu-id="b9e6a-340">**Примечание.** В поле "Целевой список" не указан порт, поэтому для перенаправления трафика от веб-сервера будет использоваться входящий порт 80 (или порт 443 для выбранной службы).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-340">**Note**: that there is no port assigned in the Target List field, thus the inbound port 80 (or 443 for the Service selected) will be used in the redirection of the web server.</span></span> <span data-ttu-id="b9e6a-341">Если веб-сервер прослушивает другой порт, к примеру порт 8080, в поле «Целевой список» можно указать значение 10.0.1.4:8080, чтобы разрешить перенаправление портов.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-341">If the web server is listening on a different port, for example port 8080, the Target List field could be updated to 10.0.1.4:8080 to allow for the Port redirection as well.</span></span>
  
    <span data-ttu-id="b9e6a-342">Следующее правило трафика приложения используется для внутренней подсети. Оно разрешает веб-серверу обращаться к серверу AppVM01 (но не AppVM02) через любую службу (Any).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-342">The next Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="b9e6a-343">![Правило AppVM01 брандмауэра][13]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="b9e6a-344">Это разрешающее правило разрешает любому серверу IIS подсети Frontend получать доступ к AppVM01 (IP-адрес 10.0.2.5) на любом порте (Any), с использованием любого протокола для доступа к данным, которые требуются веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-344">This Pass rule allows any IIS server on the Frontend subnet to reach the AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol to access data needed by the web application.</span></span>
  
    <span data-ttu-id="b9e6a-345">На этом снимке экрана в поле "Назначение" выбрано значение \<explicit-dest\> для обозначения IP-адреса 10.0.2.5 в качестве IP-адреса назначения.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-345">In this screen shot an "\<explicit-dest\>" is used in the Destination field to signify 10.0.2.5 as the destination.</span></span> <span data-ttu-id="b9e6a-346">Оно может быть либо явно указанным, как показано выше, либо называться «Сетевой объект» (как в предварительных требованиях для DNS-сервера).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-346">This could be either explicit as shown or a named Network Object (as was done in the prerequisites for the DNS server).</span></span> <span data-ttu-id="b9e6a-347">Администратор брандмауэра выбирает, какой способ использовать.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-347">This is up to the administrator of the firewall as to which method will be used.</span></span> <span data-ttu-id="b9e6a-348">Чтобы добавить IP-адрес 10.0.2.5 в качестве явного назначения, дважды щелкните первую пустую строку под значением \<explicit-dest\> и в открывшемся окне введите адрес.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-348">To add 10.0.2.5 as an Explict Desitnation, double-click on the first blank row under \<explicit-dest\> and enter the address in the window that pops up.</span></span>
  
    <span data-ttu-id="b9e6a-349">Для этого разрешающего правила не требуется NAT (преобразование сетевых адресов), так как это внутренний трафик, поэтому в поле «Способ подключения» можно установить значение «No SNAT».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-349">With this Pass Rule, no NAT is needed since this is internal traffic, so the Connection Method can be set to "No SNAT".</span></span>
  
    <span data-ttu-id="b9e6a-350">**Примечание.** В этом правиле в качестве исходной сети используется любой ресурс подсети FrontEnd. При наличии одного или определенного количества веб-серверов для большей точности можно создать ресурс "Сетевой объект" и указать конкретные IP-адреса вместо целой подсети переднего плана.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-350">**Note**: The Source network in this rule is any resource on the FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created to be more specific to those exact IP addresses instead of the entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="b9e6a-351">В этом правиле используется служба «Any» для упрощения настройки и использования примера приложения. Кроме этого разрешается ICMPv4 (проверка связи) в одном правиле.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-351">This rule uses the service “Any” to make the sample application easier to setup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="b9e6a-352">Однако так делать не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="b9e6a-353">Порты и протоколы («службы») следует сузить до минимально возможного уровня, необходимого для работы приложения, чтобы снизить возможность атак на периметре.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-353">The ports and protocols (“Services”) should be narrowed to the minimum possible that allows application operation to reduce the attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="b9e6a-354">Хотя это правило явно указывает, какое назначение используется, при настройке брандмауэра следует быть последовательными.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout the firewall configuration.</span></span> <span data-ttu-id="b9e6a-355">Рекомендуем всегда использовать именованные сетевые объекты для удобства чтения и технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-355">It is recommended that the named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="b9e6a-356">explicit-dest используется здесь только для отображения альтернативного метода ссылки. В общем, так делать не рекомендуется (особенно в сложных конфигурациях).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-356">The explicit-dest is used here only to show an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="b9e6a-357">**Правило исходящего трафика в Интернет.** Это правило разрешает передачу трафика из исходной сети в указанные сети назначения.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-357">**Outbound to Internet Rule**: This Pass rule will allow traffic from any Source network to pass to the selected Destination networks.</span></span> <span data-ttu-id="b9e6a-358">Обычно это правило уже указано на брандмауэре Barracuda NextGen Firewall по умолчанию, но оно отключено.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-358">This rule is a default rule usually already on the Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="b9e6a-359">Доступ к команде «Активировать правило» можно.получить, щелкнув этой правило правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-359">Right-clicking on this rule can access the Activate Rule command.</span></span> <span data-ttu-id="b9e6a-360">Приведенное здесь правило изменено с целью добавления двух локальных подсетей, которые созданы для примера в разделе предварительных требований этого документа для атрибута «Источник» этого правила.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-360">The rule shown here has been modified to add the two local subnets that were created as references in the prerequisite section of this document to the Source attribute of this rule.</span></span>
  
    <span data-ttu-id="b9e6a-361">![Правило исходящего трафика брандмауэра][14]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="b9e6a-362">**Правило DNS.** Это правило разрешает передавать на DNS-сервер только трафик DNS (на порт 53).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic to pass to the DNS server.</span></span> <span data-ttu-id="b9e6a-363">Для этой среды блокируется почти весь трафик от подсети FrontEnd к BackEnd, а это правило отдельно разрешает трафик DNS.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-363">For this environment most traffic from the FrontEnd to the BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="b9e6a-364">![Правило DNS брандмауэра][15]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="b9e6a-365">**Примечание.** На этом снимке экрана содержится поле "Способ подключения".</span><span class="sxs-lookup"><span data-stu-id="b9e6a-365">**Note**: In this screen shot the Connection Method is included.</span></span> <span data-ttu-id="b9e6a-366">Так как это правило применяется для трафика между внутренними IP-адресами, трансляция с помощью NAT не нужна. Соответственно, в поле «Способ подключения» установлено значение «No SNAT» для этого разрешающего правила.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-366">Because this rule is for internal IP to internal IP address traffic, no NATing is required, this the Connection Method is set to “No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="b9e6a-367">**Правило прохождения трафика между подсетями.** Это разрешающее правило установлено по умолчанию и активировано. Оно изменено для разрешения любому серверу во внутренней подсети подключаться к любому серверу в подсети переднего плана.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-367">**Subnet to Subnet Rule**: This Pass rule is a default rule that has been activated and modified to allow any server on the back end subnet to connect to any server on the front end subnet.</span></span> <span data-ttu-id="b9e6a-368">Это правило регулирует только внутренний трафик, поэтому для способа подключения можно установить значение «No SNAT».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-368">This rule is all internal traffic so the Connection Method can be set to No SNAT.</span></span>
  
    <span data-ttu-id="b9e6a-369">![Правило брандмауэра для внутреннего трафика виртуальной сети][16]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="b9e6a-370">**Примечание.** Двунаправленный флажок не установлен (как для большинства правил). Это важно для правила, так как оно применяется только к одному направлению, т. е. соединение может быть инициировано от внутренней подсети к подсети переднего плана, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-370">**Note**: The Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from the back end subnet to the front end network, but not the reverse.</span></span> <span data-ttu-id="b9e6a-371">Если установить флажок, правило будет разрешать двунаправленный трафик, а в нашей логической схеме это не требуется.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="b9e6a-372">**Правило запрета любого трафика.** Это правило всегда должно быть последним (по приоритету). Если трафик не соответствует ни одному из предыдущих правил, он будет отброшен этим правилом.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-372">**Deny All Traffic Rule**: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="b9e6a-373">Это правило обычно уже установлено по умолчанию и активировано, поэтому не требует дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="b9e6a-374">![Правило запрета брандмауэра][17]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9e6a-375">После создания всех приведенных выше правил обязательно проверьте приоритет каждого правила, чтобы разрешения и запреты трафика выполнялись надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-375">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="b9e6a-376">В этом примере правила расположены в том порядке, в котором они должны отображаться в основной сетке правил пересылки на клиенте управления Barracuda.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-376">For this example, the rules are in the order they should appear in the Main Grid of forwarding rules in the Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="b9e6a-377">Активация правил</span><span class="sxs-lookup"><span data-stu-id="b9e6a-377">Rule Activation</span></span>
<span data-ttu-id="b9e6a-378">Набор правил, после изменения в соответствии с логической схемой, необходимо отправить в брандмауэр, а затем активировать.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-378">With the ruleset modified to the specification of the logic diagram, the ruleset must be uploaded to the firewall and then activated.</span></span>

<span data-ttu-id="b9e6a-379">![Активация правила брандмауэра][18]</span><span class="sxs-lookup"><span data-stu-id="b9e6a-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="b9e6a-380">В правом верхнем углу клиента управления расположена группа кнопок.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-380">In the upper right hand corner of the management client are a cluster of buttons.</span></span> <span data-ttu-id="b9e6a-381">Нажмите кнопку "Отправить изменения", чтобы отправить измененные правила в брандмауэр, а затем нажмите кнопку "Активировать".</span><span class="sxs-lookup"><span data-stu-id="b9e6a-381">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span></span>

<span data-ttu-id="b9e6a-382">После активации набора правил брандмауэра создание среды в этом примере завершено.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-382">With the activation of the firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="b9e6a-383">Варианты прохождения трафика</span><span class="sxs-lookup"><span data-stu-id="b9e6a-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b9e6a-384">Основное, что следует запомнить: **весь** трафик будет проходить через брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-384">A key takeway is to remember that **all** traffic will come through the firewall.</span></span> <span data-ttu-id="b9e6a-385">Так, для подключения к удаленному рабочему столу сервера IIS01, даже если он находится в облачной службе Front End, и, соответственно, для доступа к подсети Front End необходимо подключиться с помощью RDP к порту 8014 брандмауэра, а затем разрешить брандмауэру отправить запрос RDP внутри сети на порт RDP IIS01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-385">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span></span> <span data-ttu-id="b9e6a-386">Кнопка «Подключиться» на портале Azure не будет работать из-за отсутствия прямого пути RDP к IIS01 (с точки зрения портала).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-386">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span></span> <span data-ttu-id="b9e6a-387">Это означает, что все подключения из Интернета будут поступать в службу безопасности и на порт, например secscv001.cloudapp.net:xxxx.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-387">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="b9e6a-388">В этих сценариях должны соблюдаться приведенные ниже правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-388">For these scenarios, the following firewall rules should be in place:</span></span>

1. <span data-ttu-id="b9e6a-389">Управление брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-389">Firewall Management</span></span>
2. <span data-ttu-id="b9e6a-390">Запрос через RDP к IIS01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-390">RDP to IIS01</span></span>
3. <span data-ttu-id="b9e6a-391">Запрос через RDP к DNS01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-391">RDP to DNS01</span></span>
4. <span data-ttu-id="b9e6a-392">Запрос через RDP к AppVM01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-392">RDP to AppVM01</span></span>
5. <span data-ttu-id="b9e6a-393">Запрос через RDP к AppVM02.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-393">RDP to AppVM02</span></span>
6. <span data-ttu-id="b9e6a-394">Трафик приложения в Интернет.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-394">App Traffic to the Web</span></span>
7. <span data-ttu-id="b9e6a-395">Трафик приложения на AppVM01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-395">App Traffic to AppVM01</span></span>
8. <span data-ttu-id="b9e6a-396">Исходящий трафик в Интернет.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-396">Outbound to the Internet</span></span>
9. <span data-ttu-id="b9e6a-397">Трафик из внутренней подсети на DNS01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-397">Frontend to DNS01</span></span>
10. <span data-ttu-id="b9e6a-398">Трафик внутри подсети (только из внутренней подсети в подсеть переднего плана).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-398">Intra-Subnet Traffic (back end to front end only)</span></span>
11. <span data-ttu-id="b9e6a-399">Запрет любого трафика.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-399">Deny All</span></span>

<span data-ttu-id="b9e6a-400">В фактическом наборе правил, скорее всего, кроме этих будет присутствовать много других правил. К тому же порядок приоритета этих правил для каждого отдельного брандмауэра будет отличаться от приведенного здесь.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-400">The actual firewall ruleset will most likely have many other rules in addition to these, the rules on any given firewall will also have different priority numbers than the ones listed here.</span></span> <span data-ttu-id="b9e6a-401">Приведенный выше нумерованный список демонстрирует соответствие между одиннадцатью правилами и их приоритетом (который определяется номерами).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-401">This list and associated numbers are to provide relevance between just these eleven rules and the relative priority amongst them.</span></span> <span data-ttu-id="b9e6a-402">Иными словами, в реальном брандмауэре «RDP на IIS01» может быть правилом номер 5, но пока оно находится ниже правила «Управление брандмауэром» и выше «RDP на DNS01», оно будет соответствовать целям этого списка.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-402">In other words; on the actual firewall, the “RDP to IIS01” may be rule number 5, but as long as it’s below the “Firewall Management” rule and above the “RDP to DNS01” rule it would align with the intention of this list.</span></span> <span data-ttu-id="b9e6a-403">Кроме того, список будет использоваться в приведенных ниже сценариях, которые разрешают подобные сокращения. Например: правило 9 брандмауэра (DNS) (FW Rule 9 (DNS)).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-403">The list will also aid in the below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="b9e6a-404">Кроме этого, для краткости четыре правила RDP будут называться «правилами RDP», если сценарий трафика не связан с RDP.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-404">Also for brevity, the four RDP rules will be collectively called, “the RDP rules” when the traffic scenario is unrelated to RDP.</span></span>

<span data-ttu-id="b9e6a-405">Помните также, что для входящего Интернет-трафика в подсетях Frontend и Backend должны быть установлены группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-405">Also recall that Network Security Groups are in-place for inbound internet traffic on the Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="b9e6a-406">Запрос из Интернета к веб-серверу (разрешено)</span><span class="sxs-lookup"><span data-stu-id="b9e6a-406">(Allowed) Internet to Web Server</span></span>
1. <span data-ttu-id="b9e6a-407">Интернет-пользователь запрашивает страницу HTTP из службы SecSvc001.CloudApp.Net (облачная служба с выходом в Интернет).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="b9e6a-408">Облачная служба передает трафик через открытую конечную точку на порте 80 на интерфейс брандмауэра 10.0.0.4:80.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-408">Cloud service passes traffic through open endpoint on port 80 to firewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="b9e6a-409">Подсети безопасности не назначены группе безопасности сети, поэтому правила группы безопасности сети системы разрешают трафик к брандмауэру.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-409">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span></span>
4. <span data-ttu-id="b9e6a-410">Трафик достигает внутреннего IP-адреса брандмауэра (10.0.1.4).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-410">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="b9e6a-411">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="b9e6a-412">Правило 1 брандмауэра (FW Mgmt) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-412">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="b9e6a-413">Правила 2–5 брандмауэра (правила RDP) не применяются — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="b9e6a-414">Правило 6 брандмауэра (приложение: Интернет) применяется — трафик разрешается, брандмауэр транслирует его с помощью NAT на 10.0.1.4 (IIS01).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it to 10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="b9e6a-415">Подсеть FrontEnd начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-415">The Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="b9e6a-416">Правило 1 группы безопасности сети (блокирование доступа к Интернету) не применяется (этот трафик транслирован с помощью NAT брандмауэром. В результате адресом источника теперь является брандмауэр, который находится в подсети безопасности. Он воспринимается группой безопасности подсети Frontend как «локальный» трафик и поэтому разрешается). Переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Frontend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span></span>
   2. <span data-ttu-id="b9e6a-417">Правила группы безопасности сети по умолчанию разрешают трафик между подсетями — трафик разрешается, дальнейшая обработка правила группы безопасности сети прекращается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-417">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="b9e6a-418">IIS01 ожидает передачу данных из Интернета, получает этот запрос и начинает его обработку.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-418">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
8. <span data-ttu-id="b9e6a-419">IIS01 пытается инициировать сеанс FTP для AppVM01 в подсети Backend.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-419">IIS01 attempts to initiates an FTP session to AppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="b9e6a-420">Определяемый пользователем маршрут в подсети Frontend следующим прыжком задает брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-420">The UDR route on Frontend subnet makes the firewall the next hop</span></span>
10. <span data-ttu-id="b9e6a-421">В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="b9e6a-422">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="b9e6a-423">Правило 1 брандмауэра (FW Mgmt) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-423">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="b9e6a-424">Правила 2–5 брандмауэра (правила RDP) не применяются — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
    3. <span data-ttu-id="b9e6a-425">Правило 6 брандмауэра (приложение: Интернет) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-425">FW Rule 6 (App: Web) doesn’t apply, move to next rule</span></span>
    4. <span data-ttu-id="b9e6a-426">Правила 7 брандмауэра (приложение: Backend) применяется, трафик разрешается — брандмауэр перенаправляет трафик на 10.0.2.5 (AppVM01).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="b9e6a-427">Подсеть BackEnd начинает обработку правил для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-427">The Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="b9e6a-428">Правило 1 группы безопасности сети (блокирование доступа к Интернету) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-428">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="b9e6a-429">Правила группы безопасности сети по умолчанию разрешают трафик между подсетями — трафик разрешается, дальнейшая обработка правила группы безопасности сети прекращается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-429">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="b9e6a-430">AppVM01 получает запрос, запускает сеанс и отвечает.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-430">AppVM01 receives the request and initiates the session and responds</span></span>
14. <span data-ttu-id="b9e6a-431">Определяемый пользователем маршрут в подсети Backend следующим прыжком задает брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-431">The UDR route on Backend subnet makes the firewall the next hop</span></span>
15. <span data-ttu-id="b9e6a-432">Так как правил для исходящего трафика в подсети Backend нет, отправка ответа разрешается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-432">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span></span>
16. <span data-ttu-id="b9e6a-433">Так как это обратный трафик в активном сеансе, брандмауэр возвращает ответ веб-серверу (IIS01).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-433">Because this is returning traffic on an established session the firewall passes the response back to the web server (IIS01)</span></span>
17. <span data-ttu-id="b9e6a-434">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="b9e6a-435">Правило 1 группы безопасности сети (блокирование доступа к Интернету) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-435">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="b9e6a-436">Правила группы безопасности сети по умолчанию разрешают трафик между подсетями — трафик разрешается, дальнейшая обработка правила группы безопасности сети прекращается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-436">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="b9e6a-437">Сервер IIS получает ответ, завершает транзакцию с AppVM01 и затем завершает создание HTTP-ответа. Этот ответ отправляется запрашивающей стороне.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-437">The IIS server receives the response, completes the transaction with AppVM01, and then completes building the HTTP response, this HTTP response is sent to the requestor</span></span>
19. <span data-ttu-id="b9e6a-438">Так как правил для исходящего трафика в подсети Frontend нет, отправка ответа разрешается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-438">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span></span>
20. <span data-ttu-id="b9e6a-439">HTTP-ответ попадает в брандмауэр. Так как это ответ активному сеансу NAT, брандмауэр его принимает.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-439">The HTTP response hits the firewall, and because this is the response to an established NAT session is accepted by the firewall</span></span>
21. <span data-ttu-id="b9e6a-440">Затем брандмауэр перенаправляет ответ обратно Интернет-пользователю.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-440">The firewall then redirects the response back to the Internet User</span></span>
22. <span data-ttu-id="b9e6a-441">Так как в подсети FrontEnd нет правил для исходящего трафика групп безопасности сети и прыжков определяемых пользователем маршрутов, отправленный ответ пропускается и Интернет-пользователь получает запрашиваемую веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-441">Since there are no outbound NSG rules or UDR hops on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-internet-rdp-to-backend"></a><span data-ttu-id="b9e6a-442">Запрос через Интернет-протокол RDP к подсети Backend (разрешено) </span><span class="sxs-lookup"><span data-stu-id="b9e6a-442">(Allowed) Internet RDP to Backend</span></span>
1. <span data-ttu-id="b9e6a-443">Администратор сервера в Интернете запрашивает сеанс RDP с AppVM01 через SecSvc001.CloudApp.Net:8025 8025 — это номер порта, назначенный для правила брандмауэра «Запрос через RDP к AppVM01».</span><span class="sxs-lookup"><span data-stu-id="b9e6a-443">Server Admin on internet requests RDP session to AppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is the user assigned port number for the “RDP to AppVM01” firewall rule</span></span>
2. <span data-ttu-id="b9e6a-444">Облачная служба передает трафик через открытую конечную точку на порте 8025 на интерфейс брандмауэра 10.0.0.4:8025.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-444">The cloud service passes traffic through the open endpoint on port 8025 to firewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="b9e6a-445">Подсети безопасности не назначены группе безопасности сети, поэтому правила группы безопасности сети системы разрешают трафик к брандмауэру.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-445">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span></span>
4. <span data-ttu-id="b9e6a-446">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="b9e6a-447">Правило 1 брандмауэра (FW Mgmt) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-447">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="b9e6a-448">Правило 2 брандмауэра (RDP IIS) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-448">FW Rule 2 (RDP IIS) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="b9e6a-449">Правило 3 брандмауэра (RDP DNS01) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-449">FW Rule 3 (RDP DNS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="b9e6a-450">Правило 4 брандмауэра (RDP AppVM01) не применяется — трафик разрешен, брандмауэр транслирует его с помощью NAT в 10.0.2.5:3389 (порт протокола RDP на AppVM01).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it to 10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="b9e6a-451">Подсеть BackEnd начинает обработку правил для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-451">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="b9e6a-452">Правило 1 группы безопасности сети (блокирование доступа к Интернету) не применяется (этот трафик транслирован с помощью NAT брандмауэром. В результате адресом источника теперь является брандмауэр, который находится в подсети безопасности. Он воспринимается группой безопасности подсети Backend как «локальный» трафик и поэтому разрешается). Переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Backend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span></span>
   2. <span data-ttu-id="b9e6a-453">Правила группы безопасности сети по умолчанию разрешают трафик между подсетями — трафик разрешается, дальнейшая обработка правила группы безопасности сети прекращается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-453">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="b9e6a-454">AppVM01 прослушивает трафик RDP и отвечает.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="b9e6a-455">Правил для исходящего трафика групп безопасности сети нет, поэтому применяются правила по умолчанию и обратный трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="b9e6a-456">Определяемые пользователем маршруты направляют исходящий трафик в брандмауэр следующим прыжком.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-456">UDR routes outbound traffic to the firewall as the next hop</span></span>
9. <span data-ttu-id="b9e6a-457">Так как это обратный трафик в активном сеансе, брандмауэр возвращает ответ пользователю Интернета.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-457">Because this is returning traffic on an established session the firewall passes the response back to the internet user</span></span>
10. <span data-ttu-id="b9e6a-458">Начинается сеанс RDP.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-458">RDP session is enabled</span></span>
11. <span data-ttu-id="b9e6a-459">Сервер AppVM01 запрашивает имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="b9e6a-460">DNS-запрос веб-сервера к серверу DNS (разрешено) </span><span class="sxs-lookup"><span data-stu-id="b9e6a-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="b9e6a-461">Веб-серверу IIS01 нужен веб-канал данных с сайта www.data.gov, но ему необходимо разрешить адрес.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="b9e6a-462">В конфигурации виртуальной сети в качестве основного DNS-сервера указан сервер DNS01 (10.0.2.4 в подсети Backend). Веб-сервер IIS01 отправляет DNS-запрос серверу DNS01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-462">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="b9e6a-463">Определяемые пользователем маршруты направляют исходящий трафик в брандмауэр следующим прыжком.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-463">UDR routes outbound traffic to the firewall as the next hop</span></span>
4. <span data-ttu-id="b9e6a-464">Так как правил для исходящего трафика в подсети Frontend для групп безопасности сети нет, трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-464">No outbound NSG rules are bound to the Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="b9e6a-465">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="b9e6a-466">Правило 1 брандмауэра (FW Mgmt) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-466">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="b9e6a-467">Правила 2–5 брандмауэра (правила RDP) не применяются — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="b9e6a-468">Правила 6–7 брандмауэра (правила приложений) не применяются — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-468">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="b9e6a-469">Правило 8 брандмауэра (к Интернету) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-469">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="b9e6a-470">Правило 9 брандмауэра (DNS) применяется, трафик разрешается — брандмауэр перенаправляет трафик на 10.0.2.4 (DNS01).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="b9e6a-471">Подсеть BackEnd начинает обработку правил для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-471">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="b9e6a-472">Правило 1 группы безопасности сети (блокирование доступа к Интернету) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-472">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="b9e6a-473">Правила группы безопасности сети по умолчанию разрешают трафик между подсетями — трафик разрешается, дальнейшая обработка правила группы безопасности сети прекращается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-473">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="b9e6a-474">DNS-сервер получает запрос.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-474">DNS server receives the request</span></span>
8. <span data-ttu-id="b9e6a-475">Указанный адрес отсутствует в кэше DNS-сервера, поэтому он отправляет запрос к корневому DNS-серверу в Интернете.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-475">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
9. <span data-ttu-id="b9e6a-476">Определяемые пользователем маршруты направляют исходящий трафик в брандмауэр следующим прыжком.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-476">UDR routes outbound traffic to the firewall as the next hop</span></span>
10. <span data-ttu-id="b9e6a-477">В подсети Backend нет правил для исходящего трафика групп безопасности сети, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="b9e6a-478">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="b9e6a-479">Правило 1 брандмауэра (FW Mgmt) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-479">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="b9e6a-480">Правила 2–5 брандмауэра (правила RDP) не применяются — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
    3. <span data-ttu-id="b9e6a-481">Правила 6–7 брандмауэра (правила приложений) не применяются — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-481">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
    4. <span data-ttu-id="b9e6a-482">Правило 8 брандмауэра (правила приложений) применяется — трафик разрешается, сеанс направляется посредством SNAT к корневому DNS-серверу в Интернете.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-482">FW Rule 8 (To Internet) does apply, traffic is allowed, session is SNAT out to root DNS server on the Internet</span></span>
12. <span data-ttu-id="b9e6a-483">DNS-сервер в Интернете отправляет ответ. Так как этот сеанс инициирован брандмауэром, он принимает ответ.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-483">Internet DNS server responds, since this session was initiated from the firewall, the response is accepted by the firewall</span></span>
13. <span data-ttu-id="b9e6a-484">Так как это активный сеанс, брандмауэр перенаправляет ответ на инициирующий сервер DNS01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-484">As this is an established session, the firewall forwards the response to the initiating server, DNS01</span></span>
14. <span data-ttu-id="b9e6a-485">Подсеть BackEnd начинает обработку правил для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-485">The Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="b9e6a-486">Правило 1 группы безопасности сети (блокирование доступа к Интернету) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-486">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="b9e6a-487">Правила группы безопасности сети по умолчанию разрешают трафик между подсетями — трафик разрешается, дальнейшая обработка правила группы безопасности сети прекращается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-487">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="b9e6a-488">DNS-сервер получает ответ, кэширует его, а затем отправляет ответ на исходный запрос на сервер IIS01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-488">The DNS server receives and caches the response, and then responds to the initial request back to IIS01</span></span>
16. <span data-ttu-id="b9e6a-489">Определяемый пользователем маршрут в подсети Backend следующим прыжком задает брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-489">The UDR route on backend subnet makes the firewall the next hop</span></span>
17. <span data-ttu-id="b9e6a-490">В подсети Backend нет правил для исходящего трафика групп безопасности сети, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-490">No outbound NSG rules exist on the Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="b9e6a-491">Это активный сеанс на брандмауэре, ответ перенаправляется брандмауэром на сервер IIS.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-491">This is an established session on the firewall, the response is forwarded by the firewall back to the IIS server</span></span>
19. <span data-ttu-id="b9e6a-492">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="b9e6a-493">Так как в группе безопасности сети нет правил, которые могут применяться ко входящему трафику из подсети Backend в подсеть Frontend, все правила группы безопасности игнорируются.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-493">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="b9e6a-494">Системное правило по умолчанию, которое разрешает трафик между подсетями, разрешает прохождение этого трафика, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-494">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
20. <span data-ttu-id="b9e6a-495">Сервер IIS01 получает ответ от сервера DNS01.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-495">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-backend-server-to-frontend-server"></a><span data-ttu-id="b9e6a-496">Запрос от тылового сервера к серверу переднего плана (разрешено)</span><span class="sxs-lookup"><span data-stu-id="b9e6a-496">(Allowed) Backend server to Frontend server</span></span>
1. <span data-ttu-id="b9e6a-497">Администратор вошел на AppVM02 через RDP и запрашивает файл непосредственно на сервере IIS01 через проводник.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-497">An administrator logged on to AppVM02 via RDP requests a file directly from the IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="b9e6a-498">Определяемый пользователем маршрут в подсети Backend следующим прыжком задает брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-498">The UDR route on Backend subnet makes the firewall the next hop</span></span>
3. <span data-ttu-id="b9e6a-499">Так как правил для исходящего трафика в подсети Backend нет, отправка ответа разрешается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-499">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span></span>
4. <span data-ttu-id="b9e6a-500">Брандмауэр начинает обработку правил.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="b9e6a-501">Правило 1 брандмауэра (FW Mgmt) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-501">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="b9e6a-502">Правила 2–5 брандмауэра (правила RDP) не применяются — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="b9e6a-503">Правила 6–7 брандмауэра (правила приложений) не применяются — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-503">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="b9e6a-504">Правило 8 брандмауэра (к Интернету) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-504">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="b9e6a-505">Правило 9 брандмауэра (DNS) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-505">FW Rule 9 (DNS) doesn’t apply, move to next rule</span></span>
   6. <span data-ttu-id="b9e6a-506">Правило 10 брандмауэра (внутри подсети) не применяется —трафик разрешается, брандмауэр передает трафик на 10.0.1.4 (IIS01).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic to 10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="b9e6a-507">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="b9e6a-508">Правило 1 группы безопасности сети (блокирование доступа к Интернету) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-508">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="b9e6a-509">Правила группы безопасности сети по умолчанию разрешают трафик между подсетями — трафик разрешается, дальнейшая обработка правила группы безопасности сети прекращается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-509">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="b9e6a-510">После аутентификации и авторизации IIS01 принимает запрос и отправляет ответ.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-510">Assuming proper authentication and authorization, IIS01 accepts the request and responds</span></span>
7. <span data-ttu-id="b9e6a-511">Определяемый пользователем маршрут в подсети Frontend следующим прыжком задает брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-511">The UDR route on Frontend subnet makes the firewall the next hop</span></span>
8. <span data-ttu-id="b9e6a-512">Так как правил для исходящего трафика в подсети Frontend нет, отправка ответа разрешается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-512">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span></span>
9. <span data-ttu-id="b9e6a-513">Так как это активный сеанс в брандмауэре, этот ответ разрешен и брандмауэр возвращает ответ AppVM02.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-513">As this is an existing session on the firewall this response is allowed and the firewall returns the response to AppVM02</span></span>
10. <span data-ttu-id="b9e6a-514">Подсеть BackEnd начинает обработку правила для входящего трафика:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="b9e6a-515">Правило 1 группы безопасности сети (блокирование доступа к Интернету) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-515">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="b9e6a-516">Правила группы безопасности сети по умолчанию разрешают трафик между подсетями — трафик разрешается, дальнейшая обработка правила группы безопасности сети прекращается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-516">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="b9e6a-517">AppVM02 получает ответ.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-517">AppVM02 receives the response</span></span>

#### <a name="denied-internet-direct-to-web-server"></a><span data-ttu-id="b9e6a-518">(Запрещено) Запрос из Интернета напрямую к веб-серверу</span><span class="sxs-lookup"><span data-stu-id="b9e6a-518">(Denied) Internet direct to Web Server</span></span>
1. <span data-ttu-id="b9e6a-519">Интернет-пользователь пытается получить доступ к веб-серверу IIS01 через службу FrontEnd001.CloudApp.Net.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-519">Internet user tries to access the web server, IIS01, through the FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="b9e6a-520">Так как для HTTP-трафика не открыты конечные точки, этот запрос не будет передан через облачную службу к серверу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-520">Since there are no endpoints open for HTTP traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="b9e6a-521">Если бы по какой-то причине конечные точки оказались открытыми, группа безопасности сети (блокирование доступа к Интернету) в подсети Frontend заблокировала бы этот трафик.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-521">If the endpoints were open for some reason, the NSG (Block Internet) on the Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="b9e6a-522">И наконец, определяемый пользователем маршрут в подсети Frontend следующим прыжком отправит весь исходящий трафик от IIS01 на брандмауэр. Брандмауэр примет его как асимметричный и отбросит исходящий трафик. Существует по крайней мере три независимых уровня защиты между Интернетом и IIS01 через облачную службу, которые предотвращают несанкционированный и несоответствующий доступ.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-522">Finally, the Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-to-backend-server"></a><span data-ttu-id="b9e6a-523">Запрос из Интернета к тыловому серверу (запрещено)</span><span class="sxs-lookup"><span data-stu-id="b9e6a-523">(Denied) Internet to Backend Server</span></span>
1. <span data-ttu-id="b9e6a-524">Интернет-пользователь пытается получить доступ к файлу на сервере AppVM01 через службу BackEnd001.CloudApp.Net.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-524">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="b9e6a-525">Так как для файлового ресурса конечные точки не открыты, этот запрос не будет передан облачной службе и не поступит на сервер.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-525">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="b9e6a-526">Если бы по какой-то причине конечные точки оказались открытыми, группа безопасности сети (блокирование доступа к Интернету) заблокировала бы этот трафик.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-526">If the endpoints were open for some reason, the NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="b9e6a-527">Наконец, определяемый пользователем маршрут следующим прыжком отправит любой исходящий трафик от AppVM01 в брандмауэр. Брандмауэр примет его как асимметричный и отбросит исходящий трафик. Таким образом, существует по крайней мере три независимых уровня защиты между Интернетом и AppVM01 через облачную службу, которые предотвращают несанкционированный и несоответствующий доступ.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-527">Finally, the UDR route would send any outbound traffic from AppVM01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-to-backend-server"></a><span data-ttu-id="b9e6a-528">Запрос от сервера переднего плана к тыловому серверу (запрещено) </span><span class="sxs-lookup"><span data-stu-id="b9e6a-528">(Denied) Frontend server to Backend Server</span></span>
1. <span data-ttu-id="b9e6a-529">Предположим, что IIS01 взломан и на нем выполняется вредоносный код, который пытается просканировать все серверы подсети Backend.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-529">Assume IIS01 was compromised and is running malicious code trying to scan the Backend subnet servers.</span></span>
2. <span data-ttu-id="b9e6a-530">Определяемый пользователем маршрут подсети Frontend следующим прыжком отправит весь исходящий трафик от IIS01 на брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-530">The Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop.</span></span> <span data-ttu-id="b9e6a-531">Взломанная виртуальная машина не может это изменить.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-531">This is not something that can be altered by the compromised VM.</span></span>
3. <span data-ttu-id="b9e6a-532">Брандмауэр будет обрабатывать трафик, если запрос отправлен к AppVM01 или DNS-серверу для проверки с помощью DNS-запросов, что трафик потенциально может быть разрешен брандмауэром (из-за правил брандмауэра 7 и 9).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-532">The firewall would process the traffic, if the request was to AppVM01, or to the DNS server for DNS lookups that traffic could potentially be allowed by the firewall (due to FW Rules 7 and 9).</span></span> <span data-ttu-id="b9e6a-533">Весь остальной трафик будет заблокирован (запрет любого трафика) правилом 11 брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="b9e6a-534">В брандмауэре может быть включено обнаружение дополнительных угроз (эта тема не рассматривается в данном документе, сведения о расширенных возможностях противостояния угрозам см. в документации поставщика своего сетевого устройства). В таком случае даже трафик, который разрешен основными правилами пересылки, описанными в этом документе, может быть запрещен, если он содержит известные подписи или шаблоны, вызывающие правило дополнительных угроз.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-534">If advanced threat detection was enabled on the firewall (which is not covered in this document, see the vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by the basic forwarding rules discussed in this document could be prevented if the traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="b9e6a-535">DNS-запрос из Интернета к серверу DNS (запрещено)</span><span class="sxs-lookup"><span data-stu-id="b9e6a-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="b9e6a-536">Пользователь Интернета пытается получить внутреннюю запись DNS на сервере DNS01 через службу BackEnd001.CloudApp.Net.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-536">Internet user tries to lookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="b9e6a-537">Так как для DNS-трафика не открыты конечные точки, этот запрос не будет передан через облачную службу к серверу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-537">Since there are no endpoints open for DNS traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="b9e6a-538">Если бы по какой-то причине конечные точки оказались открытыми, правило группы безопасности сети (блокирование доступа к Интернету) в подсети Frontend заблокировало бы этот трафик.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-538">If the endpoints were open for some reason, the NSG rule (Block Internet) on the Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="b9e6a-539">И наконец, определяемый пользователем маршрут в подсети Backend следующим прыжком отправит весь исходящий трафик от DNS01 на брандмауэр. Брандмауэр примет его как асимметричный и отбросит исходящий трафик. Существует по крайней мере три независимых уровня защиты между Интернетом и DNS01 через облачную службу, которые предотвращают несанкционированный и несоответствующий доступ.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-539">Finally, the Backend subnet UDR route would send any outbound traffic from DNS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-to-sql-access-through-firewall"></a><span data-ttu-id="b9e6a-540">Запрос данных SQL из Интернета через брандмауэр (запрещено)</span><span class="sxs-lookup"><span data-stu-id="b9e6a-540">(Denied) Internet to SQL access through Firewall</span></span>
1. <span data-ttu-id="b9e6a-541">Интернет-пользователь запрашивает данные SQL из службы SecSvc001.CloudApp.Net (облачная служба с выходом в Интернет).</span><span class="sxs-lookup"><span data-stu-id="b9e6a-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="b9e6a-542">Так как для данных SQL не открыты конечные точки, этот запрос не будет передан облачной службе и не достигнет брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-542">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="b9e6a-543">Если конечные точки SQL открыты по какой-то причине, брандмауэр начнет обработку правила:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-543">If SQL endpoints were open for some reason, the firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="b9e6a-544">Правило 1 брандмауэра (FW Mgmt) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-544">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="b9e6a-545">Правила 2–5 брандмауэра (правила RDP) не применяются — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="b9e6a-546">Правила 6 и 7 брандмауэра (правила приложения) не применяются — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-546">FW Rule 6 & 7 (Application Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="b9e6a-547">Правило 8 брандмауэра (к Интернету) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-547">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="b9e6a-548">Правило 9 брандмауэра (DNS) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-548">FW Rule 9 (DNS) doesn’t apply, move to next rule</span></span>
   6. <span data-ttu-id="b9e6a-549">Правило 10 брандмауэра (внутри подсети) не применяется — переход к следующему правилу.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move to next rule</span></span>
   7. <span data-ttu-id="b9e6a-550">Правило 11 брандмауэра (запрет любого трафика) применяется — трафик блокируется, дальнейшая обработка правил прекращается.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="b9e6a-551">Ссылки</span><span class="sxs-lookup"><span data-stu-id="b9e6a-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="b9e6a-552">Основной сценарий и конфигурация сети</span><span class="sxs-lookup"><span data-stu-id="b9e6a-552">Main Script and Network Config</span></span>
<span data-ttu-id="b9e6a-553">Сохраните полный сценарий в файл сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-553">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="b9e6a-554">Сохраните конфигурацию сети в файле с именем NetworkConf2.xml.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-554">Save the Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="b9e6a-555">При необходимости измените определенные пользователем переменные.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-555">Modify the user defined variables as needed.</span></span> <span data-ttu-id="b9e6a-556">Запустите сценарий, а затем следуйте инструкциям по настройке правил брандмауэра, приведенным выше.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-556">Run the script, then follow the Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="b9e6a-557">Полный сценарий</span><span class="sxs-lookup"><span data-stu-id="b9e6a-557">Full Script</span></span>
<span data-ttu-id="b9e6a-558">Используя определенные пользователем переменные, этот сценарий выполнит следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-558">This script will, based on the user defined variables:</span></span>

1. <span data-ttu-id="b9e6a-559">Подключение к подписке Azure</span><span class="sxs-lookup"><span data-stu-id="b9e6a-559">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="b9e6a-560">Создание новой учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="b9e6a-560">Create a new storage account</span></span>
3. <span data-ttu-id="b9e6a-561">Создаст виртуальную сеть и три подсети, которые указаны в файле конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-561">Create a new VNet and three subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="b9e6a-562">Соберет пять виртуальных машин: 1 брандмауэр и 4 виртуальных машины с Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="b9e6a-563">Настроит определяемые пользователем маршруты, включая следующее:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="b9e6a-564">Создание двух новых таблиц маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="b9e6a-565">Добавление маршрутов в таблицы.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-565">Add routes to the tables</span></span>
   3. <span data-ttu-id="b9e6a-566">Привязка таблиц к соответствующим подсетям.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-566">Bind tables to appropriate subnets</span></span>
6. <span data-ttu-id="b9e6a-567">Включит IP-пересылку на виртуальном сетевом устройстве.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-567">Enable IP Forwarding on the NVA</span></span>
7. <span data-ttu-id="b9e6a-568">Настроит группу безопасности сети:</span><span class="sxs-lookup"><span data-stu-id="b9e6a-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="b9e6a-569">Создаст группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-569">Creating a NSG</span></span>
   2. <span data-ttu-id="b9e6a-570">Добавит правило.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-570">Adding a rule</span></span>
   3. <span data-ttu-id="b9e6a-571">привяжет группу безопасности сети к соответствующим подсетям.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-571">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="b9e6a-572">Этот сценарий PowerShell должен запускаться локально на ПК или сервере, подключенном к Интернету.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9e6a-573">При запуске этого сценария могут выдаваться предупреждения и другие информационные сообщения PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="b9e6a-574">Обращать внимание следует только на сообщения об ошибках, выделенные красным цветом.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-574">Only error messages in red are cause for concern.</span></span>
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
       - One server on the FrontEnd Subnet
       - Three Servers on the BackEnd Subnet
       - IP Forwading from the FireWall out to the internet
       - User Defined Routing FrontEnd and BackEnd Subnets to the NVA

      Before running script, ensure the network configuration file is created in
      the directory referenced by $NetworkConfigFile variable (or update the
      variable to reflect the path and file name of the config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind the appropriate
      layer(s) of protection. This script serves as an example of some of the techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and the appropriate protections needed, and then effectively
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
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes to reflect your subscription and services
      # Invalid options will fail in the validation section

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
        # Note: To ensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be the NVA.

        # VM 0 - The Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - The Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - The First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - The Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - The DNS Server
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

      # Update Subscription Pointer to New Storage Account
        Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "The SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation varible is correct and the netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see the above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

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
                # Set up all the EndPoints we'll need once we're up and running
                # Note: All traffic goes through the firewall, so we'll need to set up all ports here.
                #       Also, the firewall will be redirecting traffic to a new IP and Port in a forwarding
                #       rule, so all of these endpoint have the same public and local port and the firewall
                #       will do the mapping, NATing, and/or redirection as declared in the firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when the appliance is created.
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

      # Create the Route Tables
        Write-Host "Creating the Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes to Route Tables
        Write-Host "Adding Routes to the Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate the Route Tables with the Subnets
        Write-Host "Binding Route Tables to the Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on the Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

      # Build the NSG
        Write-Host "Building the NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign the NSG to two Subnets
        # The NSG is *not* bound to the Security Subnet. The result
        # is that internet traffic flows only to the Security subnet
        # since the NSG bound to the Frontend and Backback subnets
        # will Deny internet traffic to those subnets.
        Write-Host "Binding the NSG to two subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on the IIS Server)
      # Install Backend resource (Run Post-Build Script on the AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="b9e6a-575">Файл конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="b9e6a-575">Network Config File</span></span>
<span data-ttu-id="b9e6a-576">Измените в этом XML-файле расположение и сохраните его. Затем добавьте ссылку на файл в переменную $NetworkConfigFile в приведенном выше сценарии.</span><span class="sxs-lookup"><span data-stu-id="b9e6a-576">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="b9e6a-577">Сценарии примера приложения</span><span class="sxs-lookup"><span data-stu-id="b9e6a-577">Sample Application Scripts</span></span>
<span data-ttu-id="b9e6a-578">Пример приложения для этого и других примеров сети периметра можно скачать по [этой ссылке][SampleApp].</span><span class="sxs-lookup"><span data-stu-id="b9e6a-578">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
<span data-ttu-id="b9e6a-579">[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Двунаправленная сеть периметра с виртуальным сетевым устройством, группой безопасности сети и определяемыми пользователем маршрутами"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-579">[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Bi-directional DMZ with NVA, NSG, and UDR"</span></span>
<span data-ttu-id="b9e6a-580">[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Логическое представление правил брандмауэра"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-580">[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Logical View of the Firewall Rules"</span></span>
<span data-ttu-id="b9e6a-581">[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Создание сетевого объекта FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-581">[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Create a FrontEnd Network Object"</span></span>
<span data-ttu-id="b9e6a-582">[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Создание объекта DNS-сервера"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-582">[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Create a DNS Server Object"</span></span>
<span data-ttu-id="b9e6a-583">[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Копия правила RDP по умолчанию"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-583">[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copy of Default RDP Rule"</span></span>
<span data-ttu-id="b9e6a-584">[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Правило AppVM01"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-584">[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 Rule"</span></span>
<span data-ttu-id="b9e6a-585">[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Значок перенаправления приложения"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-585">[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Application Redirect Icon"</span></span>
<span data-ttu-id="b9e6a-586">[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Значок NAT назначения"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-586">[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Destination NAT Icon"</span></span>
<span data-ttu-id="b9e6a-587">[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Значок передачи"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-587">[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Pass Icon"</span></span>
<span data-ttu-id="b9e6a-588">[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Правило управления брандмауэром"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-588">[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Firewall Management Rule"</span></span>
<span data-ttu-id="b9e6a-589">[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Правило RDP брандмауэра"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-589">[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Firewall RDP Rule"</span></span>
<span data-ttu-id="b9e6a-590">[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Правило Интернета брандмауэра"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-590">[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Firewall Web Rule"</span></span>
<span data-ttu-id="b9e6a-591">[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Правило AppVM01 брандмауэра"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-591">[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Firewall AppVM01 Rule"</span></span>
<span data-ttu-id="b9e6a-592">[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Правило исходящего трафика брандмауэра"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-592">[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Firewall Outbound Rule"</span></span>
<span data-ttu-id="b9e6a-593">[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Правило DNS брандмауэра"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-593">[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Firewall DNS Rule"</span></span>
<span data-ttu-id="b9e6a-594">[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Правило брандмауэра для внутреннего трафика виртуальной сети"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-594">[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Firewall Intra-VNet Rule"</span></span>
<span data-ttu-id="b9e6a-595">[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Правило запрета брандмауэра"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-595">[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Firewall Deny Rule"</span></span>
<span data-ttu-id="b9e6a-596">[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Активация правила брандмауэра"</span><span class="sxs-lookup"><span data-stu-id="b9e6a-596">[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Firewall Rule Activation"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
