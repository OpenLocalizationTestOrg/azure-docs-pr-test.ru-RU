---
title: "Пример DMZ-aaaAzure построения простой DMZ с Nsg | Документы Microsoft"
description: "Создание сети периметра с группами безопасности сети"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="31646-103">Пример 1 – построение простой сети периметра с использованием групп безопасности сети и классического PowerShell</span><span class="sxs-lookup"><span data-stu-id="31646-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="31646-104">[Возвращает toohello страница лучшие рекомендации безопасности границ][HOME]</span><span class="sxs-lookup"><span data-stu-id="31646-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="31646-105">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="31646-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="31646-106">Классическая модель: PowerShell</span><span class="sxs-lookup"><span data-stu-id="31646-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="31646-107">В этой статье мы создадим простую сеть периметра с четырьмя серверами Windows Server и группами безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="31646-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="31646-108">В этом примере описывается каждая из команд tooprovide hello соответствующие PowerShell более глубокого понимания каждого шага.</span><span class="sxs-lookup"><span data-stu-id="31646-108">This example describes each of hello relevant PowerShell commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="31646-109">Имеется также сценарий трафика раздел tooprovide на подробные пошаговые трафик проходит через hello уровней защиты в hello DMZ.</span><span class="sxs-lookup"><span data-stu-id="31646-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="31646-110">Наконец, в разделе references hello hello полный код и должна toobuild инструкция этот tootest среды и эксперимента с помощью различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="31646-110">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="31646-111">![Входящая сеть периметра с группой безопасности сети][1]</span><span class="sxs-lookup"><span data-stu-id="31646-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="31646-112">Описание среды</span><span class="sxs-lookup"><span data-stu-id="31646-112">Environment description</span></span>
<span data-ttu-id="31646-113">В этом примере подписки содержит hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="31646-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="31646-114">две облачные службы: FrontEnd001 и BackEnd001;</span><span class="sxs-lookup"><span data-stu-id="31646-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="31646-115">виртуальная сеть CorpNetwork с двумя подсетями (FrontEnd и BackEnd);</span><span class="sxs-lookup"><span data-stu-id="31646-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="31646-116">Сетевую группу безопасности, примененных tooboth подсети</span><span class="sxs-lookup"><span data-stu-id="31646-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="31646-117">сервер Windows Server, который представляет веб-сервер приложений (IIS01);</span><span class="sxs-lookup"><span data-stu-id="31646-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="31646-118">два сервера Windows Server, представляющих тыловые серверы приложений (AppVM01, AppVM02);</span><span class="sxs-lookup"><span data-stu-id="31646-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="31646-119">сервер Windows Server, который представляет DNS-сервер (DNS01).</span><span class="sxs-lookup"><span data-stu-id="31646-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="31646-120">В разделе "ссылки" hello имеется сценарий PowerShell, который создает большую часть среды hello, описанные в этом примере.</span><span class="sxs-lookup"><span data-stu-id="31646-120">In hello references section, there is a PowerShell script that builds most of hello environment described in this example.</span></span> <span data-ttu-id="31646-121">Построение hello ВМ и виртуальными сетями, несмотря на то, что может быть выполнено с hello пример скрипта, не подробно описаны в этом документе.</span><span class="sxs-lookup"><span data-stu-id="31646-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="31646-122">toobuild hello среды;</span><span class="sxs-lookup"><span data-stu-id="31646-122">toobuild hello environment;</span></span>

1. <span data-ttu-id="31646-123">Сохраните hello сетевой конфигурации XML-файл включаются в раздел ссылок hello (обновлено с именами, расположение и toomatch hello заданному IP адресов сценарий)</span><span class="sxs-lookup"><span data-stu-id="31646-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="31646-124">Переменные пользователя hello обновления в скрипт hello среды hello toomatch hello скрипта является toobe выполняться (подписок, имена служб, и т. д.)</span><span class="sxs-lookup"><span data-stu-id="31646-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="31646-125">Выполните сценарий hello в PowerShell</span><span class="sxs-lookup"><span data-stu-id="31646-125">Execute hello script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="31646-126">Hello область — в hello сценарий PowerShell должен соответствовать hello область — в XML-файл конфигурации сети hello.</span><span class="sxs-lookup"><span data-stu-id="31646-126">hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>
>
>

<span data-ttu-id="31646-127">После hello сценарий выполняется успешно Дополнительные необязательные действия может быть переведена в, в разделе references hello двух сценариев tooset hello веб-сервер и сервер приложений с простой web tooallow приложения, тестирование с помощью этой конфигурации сети Периметра.</span><span class="sxs-lookup"><span data-stu-id="31646-127">Once hello script runs successfully additional optional steps may be taken, in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="31646-128">Hello следующих разделах подробное описание группы безопасности сети и их использовании в этом примере при рассмотрении ключей строк сценария PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="31646-128">hello following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of hello PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="31646-129">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="31646-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="31646-130">В этом примере создается группа безопасности сети, после чего в нее загружаются шесть правил.</span><span class="sxs-lookup"><span data-stu-id="31646-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="31646-131">Вообще говоря следует сначала создать определенные правила «Разрешить», а затем последнего hello более универсальный правила «Deny».</span><span class="sxs-lookup"><span data-stu-id="31646-131">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="31646-132">Привет, назначается приоритет, определяет, какие правила вычисляются первыми.</span><span class="sxs-lookup"><span data-stu-id="31646-132">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="31646-133">После обнаружения tooapply tooa конкретного правила трафика вычисляются другим правилам.</span><span class="sxs-lookup"><span data-stu-id="31646-133">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="31646-134">Правила NSG можно применить в любом в hello входящего и исходящего направления (с точки зрения hello hello подсети).</span><span class="sxs-lookup"><span data-stu-id="31646-134">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="31646-135">Создаются декларативно, hello следующие правила для входящего трафика:</span><span class="sxs-lookup"><span data-stu-id="31646-135">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="31646-136">Внутренний трафик DNS (порт 53) разрешается.</span><span class="sxs-lookup"><span data-stu-id="31646-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="31646-137">RDP (порт 3389) из tooany Интернет hello VM-трафика</span><span class="sxs-lookup"><span data-stu-id="31646-137">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="31646-138">Может быть HTTP-трафика (порт 80) с сервера tooweb hello Интернета (IIS01)</span><span class="sxs-lookup"><span data-stu-id="31646-138">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="31646-139">Все (все порты) из IIS01 tooAppVM1-трафика</span><span class="sxs-lookup"><span data-stu-id="31646-139">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="31646-140">Любой трафик (все порты) из Интернета toohello hello запрещен всей виртуальной сети (оба подсети)</span><span class="sxs-lookup"><span data-stu-id="31646-140">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="31646-141">Любой трафик (все порты) из hello внешней подсети toohello серверной подсети запрещен</span><span class="sxs-lookup"><span data-stu-id="31646-141">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="31646-142">С подсетью привязанного tooeach эти правила, если входящие данные от hello Internet toohello веб-сервера HTTP-запроса оба правила 3 (Разрешить) и 5 (запретить) будет применен, но поскольку правило 3 обладает более высоким приоритетом только он будет применен и правила 5 бы не следует учитывать.</span><span class="sxs-lookup"><span data-stu-id="31646-142">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="31646-143">Таким образом hello HTTP-запроса допускается toohello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="31646-143">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="31646-144">Если же трафик осуществлялось tooreach hello DNS01 server, правило 5 (Deny) бы бы hello первый tooapply и hello трафик не будет разрешен toopass toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="31646-144">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="31646-145">Правила 6 (Deny) блокирует hello внешней подсети из взаимодействии подсети серверной toohello (за исключением разрешенного трафика в правилах 1 и 4), этот набор правил защищает hello серверной сети в случае, если злоумышленник взломает hello веб-приложения на hello переднего плана, злоумышленник hello бы Серверная часть «защищен» сети (только tooresources, предоставляемые на сервере hello AppVM01) toohello доступ ограничен.</span><span class="sxs-lookup"><span data-stu-id="31646-145">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="31646-146">Имеется по умолчанию правило исходящего трафика, которое разрешает трафик, исходящий toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="31646-146">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="31646-147">В этом примере мы разрешаем исходящий трафик и не меняем никаких исходящих правил.</span><span class="sxs-lookup"><span data-stu-id="31646-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="31646-148">toolock трафик в обоих направлениях маршрутизации определенные пользователя не требуется и изучены в «Пример 3» на hello [страница лучшие рекомендации безопасности границ][HOME].</span><span class="sxs-lookup"><span data-stu-id="31646-148">toolock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="31646-149">Каждое правило является более подробно следующим образом (**Примечание**: любой элемент в hello после списка, начиная со знака доллара (например: $NSGName) является определяемой пользователем переменной из скрипта hello в справочном разделе hello этого документа):</span><span class="sxs-lookup"><span data-stu-id="31646-149">Each rule is discussed in more detail as follows (**Note**: any item in hello following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="31646-150">Сначала сетевую группу безопасности должны быть построены toohold hello правила:</span><span class="sxs-lookup"><span data-stu-id="31646-150">First a Network Security Group must be built toohold hello rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="31646-151">Первое правило Hello в этом примере разрешает трафик DNS между всех внутренних сетей toohello DNS-сервера в подсети серверной hello.</span><span class="sxs-lookup"><span data-stu-id="31646-151">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="31646-152">правило Hello имеет некоторые важные параметры:</span><span class="sxs-lookup"><span data-stu-id="31646-152">hello rule has some important parameters:</span></span>
   
   * <span data-ttu-id="31646-153">Параметр Type определяет тип трафика (входящий или исходящий), к которому будет применяться правило.</span><span class="sxs-lookup"><span data-stu-id="31646-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="31646-154">Направление Hello — это с точки зрения hello hello подсети или виртуальной машины (в зависимости от того, где привязан этот NSG).</span><span class="sxs-lookup"><span data-stu-id="31646-154">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="31646-155">Таким образом Если тип — «Входящие» и трафик вводит hello подсети, hello правило будет применяться и пакетов, отправляемых hello подсети не подвержены этим правилом.</span><span class="sxs-lookup"><span data-stu-id="31646-155">Thus if Type is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="31646-156">«Приоритет» устанавливает hello порядок, в котором вычисляется поток трафика.</span><span class="sxs-lookup"><span data-stu-id="31646-156">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="31646-157">Hello hello номеров hello выше hello низкоприоритетные.</span><span class="sxs-lookup"><span data-stu-id="31646-157">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="31646-158">При определенных трафику tooa применяется правило, обрабатываются другим правилам.</span><span class="sxs-lookup"><span data-stu-id="31646-158">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="31646-159">Таким образом Если правило с приоритетом 1 разрешает трафик и правило с приоритетом 2 запрещает трафика и применяются оба правила tootraffic то трафика hello допускается tooflow (поскольку правило 1 имеет более высокий приоритет он действует и дополнительные правила не были применены).</span><span class="sxs-lookup"><span data-stu-id="31646-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="31646-160">Параметр Action определяет, что нужно делать с трафиком, который подпадает под действие правила, — запретить или разрешить.</span><span class="sxs-lookup"><span data-stu-id="31646-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="31646-161">Это правило позволяет tooflow трафик RDP из hello toohello Интернет RDP-порту на любом сервере в hello привязан подсети.</span><span class="sxs-lookup"><span data-stu-id="31646-161">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> <span data-ttu-id="31646-162">В правиле используется два специальных типа адресных префиксов, VIRTUAL_NETWORK и INTERNET,</span><span class="sxs-lookup"><span data-stu-id="31646-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="31646-163">Эти теги являются легко tooaddress большего категории префиксов адресов.</span><span class="sxs-lookup"><span data-stu-id="31646-163">These tags are an easy way tooaddress a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="31646-164">Это правило разрешает входящий трафик toohit hello веб-сервер IIS.</span><span class="sxs-lookup"><span data-stu-id="31646-164">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="31646-165">Это правило не приводит к изменению поведения маршрутизации hello.</span><span class="sxs-lookup"><span data-stu-id="31646-165">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="31646-166">правило Hello допускает только трафик, предназначенный для IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="31646-166">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="31646-167">Таким образом Если трафика из Интернета hello имел hello веб-сервер в качестве места назначения, это правило будет разрешено и остановить обработку Дополнительные правила.</span><span class="sxs-lookup"><span data-stu-id="31646-167">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="31646-168">(В hello правило с приоритетом 140 все другие этот трафик блокируется).</span><span class="sxs-lookup"><span data-stu-id="31646-168">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="31646-169">Если только обработку HTTP-трафика, это правило может быть дальнейших ограниченных tooonly разрешить конечный порт 80.</span><span class="sxs-lookup"><span data-stu-id="31646-169">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="31646-170">Это правило позволяет toopass трафик от сервера hello IIS01 toohello AppVM01 сервера, более поздней версии правило блокирует весь остальной трафик tooBackend переднего плана.</span><span class="sxs-lookup"><span data-stu-id="31646-170">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="31646-171">tooimprove, это правило, если порт hello известно, что должны быть добавлены.</span><span class="sxs-lookup"><span data-stu-id="31646-171">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="31646-172">Например, если сервер IIS hello попадание SQL Server на AppVM01, диапазон портов назначения hello должен измениться с «*» (Any) too1433 (hello порт сервера SQL) таким образом позволяя меньшего размера входящего атак на AppVM01 следует hello веб-приложение будет скомпрометирован.</span><span class="sxs-lookup"><span data-stu-id="31646-172">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="31646-173">Это правило запрещает трафик от Интернет-серверы tooany hello hello сети.</span><span class="sxs-lookup"><span data-stu-id="31646-173">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="31646-174">Правилам hello с приоритетом 110 и 120 hello эффект tooallow только входящий трафик toohello брандмауэр и порты протокола удаленного рабочего СТОЛА на серверах и блокирует все остальное.</span><span class="sxs-lookup"><span data-stu-id="31646-174">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="31646-175">Это правило является «резервным» правило tooblock все потоки Непредвиденная.</span><span class="sxs-lookup"><span data-stu-id="31646-175">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="31646-176">Hello окончательного правило запрещает трафик от hello внешней подсети toohello серверной подсети.</span><span class="sxs-lookup"><span data-stu-id="31646-176">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="31646-177">Поскольку это правило является только правила входящего трафика, обратный трафик (от toohello серверной hello переднего плана).</span><span class="sxs-lookup"><span data-stu-id="31646-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="31646-178">Варианты прохождения трафика</span><span class="sxs-lookup"><span data-stu-id="31646-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="31646-179">(*Разрешено*) tooweb Интернет-сервера</span><span class="sxs-lookup"><span data-stu-id="31646-179">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="31646-180">Интернет-пользователь запрашивает страницу HTTP от FrontEnd001.CloudApp.Net (облачная служба, открытая для доступа из Интернета)</span><span class="sxs-lookup"><span data-stu-id="31646-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="31646-181">Облачные службы передает трафик через открытую конечную точку на порт 80 по направлению к IIS01 (hello веб-сервера)</span><span class="sxs-lookup"><span data-stu-id="31646-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="31646-182">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="31646-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="31646-183">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-183">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="31646-184">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-184">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="31646-185">Применить правила NSG 3 (tooIIS01 Интернет), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="31646-185">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="31646-186">Трафик достигнет внутренний IP-адрес веб-сервера hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="31646-186">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="31646-187">IIS01 прослушивание веб-трафик, получает этот запрос и начинает обработку запроса hello</span><span class="sxs-lookup"><span data-stu-id="31646-187">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="31646-188">IIS01 запрашивает hello SQL Server на AppVM01 сведения</span><span class="sxs-lookup"><span data-stu-id="31646-188">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="31646-189">В подсети Frontend нет правил для обработки исходящего трафика, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="31646-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="31646-190">подсети серверной Hello начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="31646-190">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="31646-191">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-191">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="31646-192">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-192">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="31646-193">Правила NSG 3 (Internet tooFirewall) не применяется, переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-193">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="31646-194">Применить правила NSG 4 (IIS01 tooAppVM01), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="31646-194">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="31646-195">AppVM01 получает hello SQL-запрос и ответ</span><span class="sxs-lookup"><span data-stu-id="31646-195">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="31646-196">Поскольку имеются правила для исходящих подключений hello серверной подсети, может быть hello ответа</span><span class="sxs-lookup"><span data-stu-id="31646-196">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="31646-197">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="31646-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="31646-198">Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены</span><span class="sxs-lookup"><span data-stu-id="31646-198">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="31646-199">правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello.</span><span class="sxs-lookup"><span data-stu-id="31646-199">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="31646-200">Получает ответ SQL hello и завершения hello HTTP-ответ и отправляет запрашивающей стороны toohello Hello сервера IIS</span><span class="sxs-lookup"><span data-stu-id="31646-200">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
13. <span data-ttu-id="31646-201">Так как имеются правила для исходящих подключений в интерфейсной подсети hello hello ответа может быть и hello Интернета пользователь получает hello веб-страницы при запросе.</span><span class="sxs-lookup"><span data-stu-id="31646-201">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="31646-202">(*Разрешено*) toobackend протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="31646-202">(*Allowed*) RDP toobackend</span></span>
1. <span data-ttu-id="31646-203">Администратор сервера в Интернете запрашивает tooAppVM01 сеанс RDP в BackEnd001.CloudApp.Net:xxxxx, где xxxxx-hello случайным образом назначенный номер порта для протокола удаленного рабочего СТОЛА tooAppVM01 (hello назначенный порт можно найти на hello портал Azure или с помощью PowerShell)</span><span class="sxs-lookup"><span data-stu-id="31646-203">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="31646-204">Подсеть BackEnd начинает обработку правила для входящего трафика:</span><span class="sxs-lookup"><span data-stu-id="31646-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="31646-205">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-205">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="31646-206">Правило 2 группы безопасности сети (RDP) применяется — трафик разрешается, дальнейшая обработка правил прекращается.</span><span class="sxs-lookup"><span data-stu-id="31646-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="31646-207">Правил для исходящего трафика нет, поэтому применяются правила по умолчанию и обратный трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="31646-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="31646-208">Начинается сеанс RDP.</span><span class="sxs-lookup"><span data-stu-id="31646-208">RDP session is enabled</span></span>
5. <span data-ttu-id="31646-209">Запрашивает AppVM01 hello имя пользователя и пароль</span><span class="sxs-lookup"><span data-stu-id="31646-209">AppVM01 prompts for hello user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="31646-210">DNS-запрос веб-сервера к серверу DNS (*разрешено*)</span><span class="sxs-lookup"><span data-stu-id="31646-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="31646-211">Веб-сервера, IIS01, потребности в www.data.gov, но потребности tooresolve hello адрес канала данных.</span><span class="sxs-lookup"><span data-stu-id="31646-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="31646-212">Hello конфигурацию сети для виртуальной сети hello списков DNS01 (10.0.2.4 подсети hello серверной части) как hello основной DNS-сервер, IIS01 отправляет запрос tooDNS01 hello DNS</span><span class="sxs-lookup"><span data-stu-id="31646-212">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="31646-213">В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="31646-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="31646-214">Подсеть BackEnd начинает обработку входящего правила:</span><span class="sxs-lookup"><span data-stu-id="31646-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="31646-215">Правило 1 группы безопасности сети (DNS) применяется — трафик разрешается, дальнейшая обработка правил прекращается.</span><span class="sxs-lookup"><span data-stu-id="31646-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="31646-216">DNS-сервер получает запрос hello</span><span class="sxs-lookup"><span data-stu-id="31646-216">DNS server receives hello request</span></span>
6. <span data-ttu-id="31646-217">DNS-сервер не имеет адреса hello в кэше и запрашивает у корневой сервер DNS на hello Интернета</span><span class="sxs-lookup"><span data-stu-id="31646-217">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="31646-218">В подсети BackEnd нет правил для исходящего трафика, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="31646-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="31646-219">Internet DNS-сервер отвечает, поскольку этот сеанс был инициирован внутренне, допускается hello ответа</span><span class="sxs-lookup"><span data-stu-id="31646-219">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="31646-220">DNS-сервер кэширует ответ hello и реагирует назад tooIIS01 toohello исходного запроса</span><span class="sxs-lookup"><span data-stu-id="31646-220">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="31646-221">В подсети BackEnd нет правил для исходящего трафика, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="31646-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="31646-222">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="31646-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="31646-223">Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены</span><span class="sxs-lookup"><span data-stu-id="31646-223">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="31646-224">правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello</span><span class="sxs-lookup"><span data-stu-id="31646-224">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="31646-225">IIS01 получает hello ответа от DNS01</span><span class="sxs-lookup"><span data-stu-id="31646-225">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="31646-226">Обращение веб-сервера к файлу на сервере AppVM01 (*разрешено*)</span><span class="sxs-lookup"><span data-stu-id="31646-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="31646-227">IIS01 запрашивает файл на AppVM01</span><span class="sxs-lookup"><span data-stu-id="31646-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="31646-228">В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="31646-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="31646-229">подсети серверной Hello начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="31646-229">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="31646-230">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-230">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="31646-231">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-231">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="31646-232">Правила NSG 3 (Internet tooIIS01) не применяется, переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-232">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="31646-233">Применить правила NSG 4 (IIS01 tooAppVM01), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="31646-233">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="31646-234">AppVM01 получает запрос hello и высылает файла (при условии, что права доступа)</span><span class="sxs-lookup"><span data-stu-id="31646-234">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="31646-235">Поскольку имеются правила для исходящих подключений hello серверной подсети, может быть hello ответа</span><span class="sxs-lookup"><span data-stu-id="31646-235">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="31646-236">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="31646-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="31646-237">Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены</span><span class="sxs-lookup"><span data-stu-id="31646-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="31646-238">правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello.</span><span class="sxs-lookup"><span data-stu-id="31646-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="31646-239">сервер IIS Hello получает файл hello</span><span class="sxs-lookup"><span data-stu-id="31646-239">hello IIS server receives hello file</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="31646-240">(*Отказано в доступе*) toobackend веб-сервера</span><span class="sxs-lookup"><span data-stu-id="31646-240">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="31646-241">Пользователь Интернета пытается tooaccess файл на AppVM01 через hello BackEnd001.CloudApp.Net службы</span><span class="sxs-lookup"><span data-stu-id="31646-241">An internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="31646-242">Поскольку конечные точки не открыты для общего файлового ресурса, этот трафик не будет передан hello облачной службы и не достигают сервера hello</span><span class="sxs-lookup"><span data-stu-id="31646-242">Since there are no endpoints open for file share, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="31646-243">Если по некоторым причинам hello конечные точки были открыты, правило NSG 5 (Internet tooVNet) заблокирует этот трафик</span><span class="sxs-lookup"><span data-stu-id="31646-243">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="31646-244">DNS-запрос из Интернета к серверу DNS (*запрещено*)</span><span class="sxs-lookup"><span data-stu-id="31646-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="31646-245">Пользователь Интернета пытается toolook копирование внутренние DNS-запись на DNS01 через hello BackEnd001.CloudApp.Net службы</span><span class="sxs-lookup"><span data-stu-id="31646-245">An internet user tries toolook up an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="31646-246">Поскольку конечные точки не открыты для DNS, трафик не будет передан hello облачной службы и не достигают сервера hello</span><span class="sxs-lookup"><span data-stu-id="31646-246">Since there are no endpoints open for DNS, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="31646-247">Если по некоторым причинам hello конечные точки были открыты, правило NSG 5 (Internet tooVNet) заблокирует этот трафик (Примечание: 1 правило (DNS) не будут применяться по двум причинам, исходный адрес первого hello hello Интернета, это правило применяется только toohello также виртуальной локальной сети как hello источника Это правило является разрешающее правило, поэтому она никогда не будет запрещать трафик)</span><span class="sxs-lookup"><span data-stu-id="31646-247">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="31646-248">(*Отказано в доступе*) Web access tooSQL через брандмауэр</span><span class="sxs-lookup"><span data-stu-id="31646-248">(*Denied*) Web tooSQL access through firewall</span></span>
1. <span data-ttu-id="31646-249">Интернет-пользователь запрашивает данные SQL из FrontEnd001.CloudApp.Net (облачная служба, открытая для доступа через Интернет)</span><span class="sxs-lookup"><span data-stu-id="31646-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="31646-250">Поскольку конечные точки не открыты для SQL, такой трафик не будет передан hello облачной службы и не достичь hello брандмауэра</span><span class="sxs-lookup"><span data-stu-id="31646-250">Since there are no endpoints open for SQL, this traffic would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="31646-251">Если конечные точки были открыты для какой-либо причине, hello внешней подсети начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="31646-251">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="31646-252">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-252">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="31646-253">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="31646-253">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="31646-254">Применить правила NSG 3 (tooIIS01 Интернет), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="31646-254">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="31646-255">Трафик достигнет внутренний IP-адрес hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="31646-255">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="31646-256">IIS01 не прослушивает порт 1433, без запроса toohello ответа</span><span class="sxs-lookup"><span data-stu-id="31646-256">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="31646-257">Заключение</span><span class="sxs-lookup"><span data-stu-id="31646-257">Conclusion</span></span>
<span data-ttu-id="31646-258">В этом примере является относительно простой и простым способом изоляции hello внутренней подсети из входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="31646-258">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="31646-259">Дополнительные примеры и общие сведения о периметре безопасности сети можно найти [здесь][HOME].</span><span class="sxs-lookup"><span data-stu-id="31646-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="31646-260">Ссылки</span><span class="sxs-lookup"><span data-stu-id="31646-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="31646-261">Основной сценарий и конфигурация сети</span><span class="sxs-lookup"><span data-stu-id="31646-261">Main script and network config</span></span>
<span data-ttu-id="31646-262">Сохраните hello полный скрипт в файл скрипта PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31646-262">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="31646-263">Сохранить hello сетевой конфигурации в файл с именем «NetworkConf1.xml.»</span><span class="sxs-lookup"><span data-stu-id="31646-263">Save hello Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="31646-264">Изменение определяемых пользователем переменных hello как hello необходимые и выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="31646-264">Modify hello user-defined variables as needed and run hello script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="31646-265">Полный сценарий</span><span class="sxs-lookup"><span data-stu-id="31646-265">Full script</span></span>
<span data-ttu-id="31646-266">Этот скрипт будет на основе hello определяемых пользователем переменных;</span><span class="sxs-lookup"><span data-stu-id="31646-266">This script will, based on hello user-defined variables;</span></span>

1. <span data-ttu-id="31646-267">Подключение tooan подписки Azure</span><span class="sxs-lookup"><span data-stu-id="31646-267">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="31646-268">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="31646-268">Create a storage account</span></span>
3. <span data-ttu-id="31646-269">Создание виртуальной сети и две подсети, как определено в файле конфигурации сети hello</span><span class="sxs-lookup"><span data-stu-id="31646-269">Create a VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="31646-270">Создаст четыре сервера виртуальных машин под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="31646-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="31646-271">Настроит группу безопасности сети:</span><span class="sxs-lookup"><span data-stu-id="31646-271">Configure NSG including:</span></span>
   * <span data-ttu-id="31646-272">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="31646-272">Creating an NSG</span></span>
   * <span data-ttu-id="31646-273">добавит в нее правила;</span><span class="sxs-lookup"><span data-stu-id="31646-273">Populating it with rules</span></span>
   * <span data-ttu-id="31646-274">Привязка hello NSG toohello соответствующие подсети</span><span class="sxs-lookup"><span data-stu-id="31646-274">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="31646-275">Этот сценарий PowerShell должен запускаться локально на ПК или сервере, подключенном к Интернету.</span><span class="sxs-lookup"><span data-stu-id="31646-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31646-276">При запуске этого сценария могут выдаваться предупреждения и другие информационные сообщения PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31646-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="31646-277">Обращать внимание следует только на сообщения об ошибках, выделенные красным цветом.</span><span class="sxs-lookup"><span data-stu-id="31646-277">Only error messages in red are cause for concern.</span></span>
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

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

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="31646-278">Файл конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="31646-278">Network config file</span></span>
<span data-ttu-id="31646-279">Сохраните этот файл xml с новое местоположение и добавьте переменной toohello $NetworkConfigFile файл toothis link hello в hello предшествующий скрипта.</span><span class="sxs-lookup"><span data-stu-id="31646-279">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello preceding script.</span></span>

```XML
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
```

#### <a name="sample-application-scripts"></a><span data-ttu-id="31646-280">Примеры сценариев приложения</span><span class="sxs-lookup"><span data-stu-id="31646-280">Sample application scripts</span></span>
<span data-ttu-id="31646-281">При желании tooinstall образец приложения для этого и других примерах DMZ, оно предоставлено в hello по ссылке: [образец приложения скрипта][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="31646-281">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="31646-282">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31646-282">Next steps</span></span>
* <span data-ttu-id="31646-283">Обновите и сохраните XML-файл</span><span class="sxs-lookup"><span data-stu-id="31646-283">Update and save XML file</span></span>
* <span data-ttu-id="31646-284">Запустите среду hello toobuild сценария PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="31646-284">Run hello PowerShell script toobuild hello environment</span></span>
* <span data-ttu-id="31646-285">Установите пример приложения hello</span><span class="sxs-lookup"><span data-stu-id="31646-285">Install hello sample application</span></span>
* <span data-ttu-id="31646-286">Проверьте прохождение разных потоков трафика через эту сеть периметра.</span><span class="sxs-lookup"><span data-stu-id="31646-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Входящая сеть периметра с группой безопасности сети"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

