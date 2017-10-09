---
title: "Пример DMZ-aaaAzure построения простой DMZ с Nsg | Документы Microsoft"
description: "Создание сети периметра с группами безопасности сети"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="acfec-103">Пример 1. Создание сети периметра с группами безопасности сети с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acfec-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="acfec-104">[Возвращает toohello страница лучшие рекомендации безопасности границ][HOME]</span><span class="sxs-lookup"><span data-stu-id="acfec-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="acfec-105">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="acfec-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="acfec-106">Классическая модель: PowerShell</span><span class="sxs-lookup"><span data-stu-id="acfec-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="acfec-107">В этой статье мы создадим простую сеть периметра с четырьмя серверами Windows Server и группами безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="acfec-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="acfec-108">В этом примере описаны hello подходящий шаблон разделы tooprovide более глубокого понимания каждого шага.</span><span class="sxs-lookup"><span data-stu-id="acfec-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="acfec-109">Имеется также tooprovide раздел сценария трафика пошаговые углубленные как трафик проходит через hello уровней защиты в сети Периметра hello.</span><span class="sxs-lookup"><span data-stu-id="acfec-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="acfec-110">Наконец в разделе "ссылки" hello является toobuild hello полный шаблон кода и инструкции, этот tootest среды и эксперимента с помощью различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="acfec-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="acfec-111">![Входящая сеть периметра с группой безопасности сети][1]</span><span class="sxs-lookup"><span data-stu-id="acfec-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="acfec-112">Описание среды</span><span class="sxs-lookup"><span data-stu-id="acfec-112">Environment description</span></span>
<span data-ttu-id="acfec-113">В этом примере подписки содержит hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="acfec-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="acfec-114">одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="acfec-114">A single resource group</span></span>
* <span data-ttu-id="acfec-115">виртуальную сеть с двумя подсетями (интерфейсной и внутренней);</span><span class="sxs-lookup"><span data-stu-id="acfec-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="acfec-116">Сетевую группу безопасности, примененных tooboth подсети</span><span class="sxs-lookup"><span data-stu-id="acfec-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="acfec-117">сервер Windows Server, который представляет веб-сервер приложений (IIS01);</span><span class="sxs-lookup"><span data-stu-id="acfec-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="acfec-118">два сервера Windows Server, представляющих тыловые серверы приложений (AppVM01, AppVM02);</span><span class="sxs-lookup"><span data-stu-id="acfec-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="acfec-119">сервер Windows Server, который представляет DNS-сервер (DNS01).</span><span class="sxs-lookup"><span data-stu-id="acfec-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="acfec-120">Общедоступный IP-адрес, связанный с веб-сервера приложения hello</span><span class="sxs-lookup"><span data-stu-id="acfec-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="acfec-121">В разделе "ссылки" hello отсутствует ссылка tooan Azure шаблона диспетчера ресурсов, создающий среду hello, описанные в этом примере.</span><span class="sxs-lookup"><span data-stu-id="acfec-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="acfec-122">Построение hello ВМ и виртуальными сетями, несмотря на то, что выполнено шаблоном пример hello не подробно описаны в этом документе.</span><span class="sxs-lookup"><span data-stu-id="acfec-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="acfec-123">**toobuild этой среды** (подробные инструкции находятся в разделе references hello этого документа);</span><span class="sxs-lookup"><span data-stu-id="acfec-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="acfec-124">Развертывание hello шаблона Azure Resource Manager в: [шаблоны быстрый запуск Azure][Template]</span><span class="sxs-lookup"><span data-stu-id="acfec-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="acfec-125">Установите образец приложения hello: [образец приложения скрипта][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="acfec-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="acfec-126">tooRDP tooany серверы в этом экземпляре сервера IIS hello используется в качестве «переход поля».</span><span class="sxs-lookup"><span data-stu-id="acfec-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="acfec-127">Первый сервер IIS toohello RDP и затем с сервера hello серверной части toohello RDP сервера IIS.</span><span class="sxs-lookup"><span data-stu-id="acfec-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="acfec-128">В качестве альтернативы можно связать общедоступный IP-адрес с каждым сетевым адаптером сервера для упрощения подключения через RDP.</span><span class="sxs-lookup"><span data-stu-id="acfec-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="acfec-129">Hello следующих разделах приводится подробное описание hello сетевой группы безопасности и как он работает в этом примере при рассмотрении ключа строки hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="acfec-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="acfec-130">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="acfec-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="acfec-131">В этом примере создается группа безопасности сети, после чего в нее загружаются шесть правил.</span><span class="sxs-lookup"><span data-stu-id="acfec-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="acfec-132">Вообще говоря следует сначала создать определенные правила «Разрешить», а затем последнего hello более универсальный правила «Deny».</span><span class="sxs-lookup"><span data-stu-id="acfec-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="acfec-133">Привет, назначается приоритет, определяет, какие правила вычисляются первыми.</span><span class="sxs-lookup"><span data-stu-id="acfec-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="acfec-134">После обнаружения tooapply tooa конкретного правила трафика вычисляются другим правилам.</span><span class="sxs-lookup"><span data-stu-id="acfec-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="acfec-135">Правила NSG можно применить в любом в hello входящего и исходящего направления (с точки зрения hello hello подсети).</span><span class="sxs-lookup"><span data-stu-id="acfec-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="acfec-136">Создаются декларативно, hello следующие правила для входящего трафика:</span><span class="sxs-lookup"><span data-stu-id="acfec-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="acfec-137">Внутренний трафик DNS (порт 53) разрешается.</span><span class="sxs-lookup"><span data-stu-id="acfec-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="acfec-138">RDP (порт 3389) из tooany Интернет hello VM-трафика</span><span class="sxs-lookup"><span data-stu-id="acfec-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="acfec-139">Может быть HTTP-трафика (порт 80) с сервера tooweb hello Интернета (IIS01)</span><span class="sxs-lookup"><span data-stu-id="acfec-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="acfec-140">Все (все порты) из IIS01 tooAppVM1-трафика</span><span class="sxs-lookup"><span data-stu-id="acfec-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="acfec-141">Любой трафик (все порты) из Интернета toohello hello запрещен всей виртуальной сети (оба подсети)</span><span class="sxs-lookup"><span data-stu-id="acfec-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="acfec-142">Любой трафик (все порты) из hello внешней подсети toohello серверной подсети запрещен</span><span class="sxs-lookup"><span data-stu-id="acfec-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="acfec-143">С подсетью привязанного tooeach эти правила, если входящие данные от hello Internet toohello веб-сервера HTTP-запроса оба правила 3 (Разрешить) и 5 (запретить) будет применен, но поскольку правило 3 обладает более высоким приоритетом только он будет применен и правила 5 бы не следует учитывать.</span><span class="sxs-lookup"><span data-stu-id="acfec-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="acfec-144">Таким образом hello HTTP-запроса допускается toohello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="acfec-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="acfec-145">Если же трафик осуществлялось tooreach hello DNS01 server, правило 5 (Deny) бы бы hello первый tooapply и hello трафик не будет разрешен toopass toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="acfec-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="acfec-146">Правила 6 (Deny) блокирует hello внешней подсети из взаимодействии подсети серверной toohello (за исключением разрешенного трафика в правилах 1 и 4), этот набор правил защищает hello серверной сети в случае, если злоумышленник взломает hello веб-приложения на hello переднего плана, злоумышленник hello бы Серверная часть «защищен» сети (только tooresources, предоставляемые на сервере hello AppVM01) toohello доступ ограничен.</span><span class="sxs-lookup"><span data-stu-id="acfec-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="acfec-147">Имеется по умолчанию правило исходящего трафика, которое разрешает трафик, исходящий toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="acfec-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="acfec-148">В этом примере мы разрешаем исходящий трафик и не меняем никаких исходящих правил.</span><span class="sxs-lookup"><span data-stu-id="acfec-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="acfec-149">tooapply tootraffic политики безопасности в обоих направлениях, маршрутизации определенные пользователя не требуется и изучены в «Пример 3» на hello [страница лучшие рекомендации безопасности границ][HOME].</span><span class="sxs-lookup"><span data-stu-id="acfec-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="acfec-150">Ниже приведены пояснения по каждому правилу.</span><span class="sxs-lookup"><span data-stu-id="acfec-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="acfec-151">Ресурс группы безопасности сети должен быть экземпляр toohold hello правила:</span><span class="sxs-lookup"><span data-stu-id="acfec-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="acfec-152">Первое правило Hello в этом примере разрешает трафик DNS между всех внутренних сетей toohello DNS-сервера в подсети серверной hello.</span><span class="sxs-lookup"><span data-stu-id="acfec-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="acfec-153">правило Hello имеет некоторые важные параметры:</span><span class="sxs-lookup"><span data-stu-id="acfec-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="acfec-154">«destinationAddressPrefix» - правила можно использовать специальный тип префикс адреса, называется «по умолчанию тег», эти теги — это системные идентификаторы, позволяющие легко tooaddress большего категории префиксов адресов.</span><span class="sxs-lookup"><span data-stu-id="acfec-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="acfec-155">Это правило использует hello тег по умолчанию «Internet» toosignify среди адресов за пределами hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="acfec-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="acfec-156">Другие метки префиксов — VirtualNetwork и AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="acfec-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="acfec-157">Параметр Direction определяет тип трафика (входящий или исходящий), к которому будет применяться правило.</span><span class="sxs-lookup"><span data-stu-id="acfec-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="acfec-158">Направление Hello — это с точки зрения hello hello подсети или виртуальной машины (в зависимости от того, где привязан этот NSG).</span><span class="sxs-lookup"><span data-stu-id="acfec-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="acfec-159">Таким образом если направление — «Входящие» и трафик вводит hello подсети, hello правило будет применяться и пакетов, отправляемых hello подсети не подвержены этим правилом.</span><span class="sxs-lookup"><span data-stu-id="acfec-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="acfec-160">«Приоритет» устанавливает hello порядок, в котором вычисляется поток трафика.</span><span class="sxs-lookup"><span data-stu-id="acfec-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="acfec-161">Hello hello номеров hello выше hello низкоприоритетные.</span><span class="sxs-lookup"><span data-stu-id="acfec-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="acfec-162">При определенных трафику tooa применяется правило, обрабатываются другим правилам.</span><span class="sxs-lookup"><span data-stu-id="acfec-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="acfec-163">Таким образом Если правило с приоритетом 1 разрешает трафик и правило с приоритетом 2 запрещает трафика и применяются оба правила tootraffic то трафика hello допускается tooflow (поскольку правило 1 имеет более высокий приоритет он действует и дополнительные правила не были применены).</span><span class="sxs-lookup"><span data-stu-id="acfec-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="acfec-164">Параметр Access определяет, что нужно делать с трафиком, который подпадает под действие правила: запретить (Deny) или разрешить (Allow).</span><span class="sxs-lookup"><span data-stu-id="acfec-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="acfec-165">Это правило позволяет tooflow трафик RDP из hello toohello Интернет RDP-порту на любом сервере в hello привязан подсети.</span><span class="sxs-lookup"><span data-stu-id="acfec-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="acfec-166">Это правило разрешает входящий трафик toohit hello веб-сервер IIS.</span><span class="sxs-lookup"><span data-stu-id="acfec-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="acfec-167">Это правило не приводит к изменению поведения маршрутизации hello.</span><span class="sxs-lookup"><span data-stu-id="acfec-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="acfec-168">правило Hello допускает только трафик, предназначенный для IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="acfec-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="acfec-169">Таким образом Если трафика из Интернета hello имел hello веб-сервер в качестве места назначения, это правило будет разрешено и остановить обработку Дополнительные правила.</span><span class="sxs-lookup"><span data-stu-id="acfec-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="acfec-170">(В hello правило с приоритетом 140 все другие этот трафик блокируется).</span><span class="sxs-lookup"><span data-stu-id="acfec-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="acfec-171">Если только обработку HTTP-трафика, это правило может быть дальнейших ограниченных tooonly разрешить конечный порт 80.</span><span class="sxs-lookup"><span data-stu-id="acfec-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="acfec-172">Это правило позволяет toopass трафик от сервера hello IIS01 toohello AppVM01 сервера, более поздней версии правило блокирует весь остальной трафик tooBackend переднего плана.</span><span class="sxs-lookup"><span data-stu-id="acfec-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="acfec-173">tooimprove, это правило, если порт hello известно, что должны быть добавлены.</span><span class="sxs-lookup"><span data-stu-id="acfec-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="acfec-174">Например, если сервер IIS hello попадание SQL Server на AppVM01, диапазон портов назначения hello должен измениться с «*» (Any) too1433 (hello порт сервера SQL) таким образом позволяя меньшего размера входящего атак на AppVM01 следует hello веб-приложение будет скомпрометирован.</span><span class="sxs-lookup"><span data-stu-id="acfec-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="acfec-175">Это правило запрещает трафик от Интернет-серверы tooany hello hello сети.</span><span class="sxs-lookup"><span data-stu-id="acfec-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="acfec-176">Правилам hello с приоритетом 110 и 120 hello эффект tooallow только входящий трафик toohello брандмауэр и порты протокола удаленного рабочего СТОЛА на серверах и блокирует все остальное.</span><span class="sxs-lookup"><span data-stu-id="acfec-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="acfec-177">Это правило является «резервным» правило tooblock все потоки Непредвиденная.</span><span class="sxs-lookup"><span data-stu-id="acfec-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="acfec-178">Hello окончательного правило запрещает трафик от hello внешней подсети toohello серверной подсети.</span><span class="sxs-lookup"><span data-stu-id="acfec-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="acfec-179">Поскольку это правило является только правила входящего трафика, обратный трафик (от toohello серверной hello переднего плана).</span><span class="sxs-lookup"><span data-stu-id="acfec-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="acfec-180">Варианты прохождения трафика</span><span class="sxs-lookup"><span data-stu-id="acfec-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="acfec-181">(*Разрешено*) tooweb Интернет-сервера</span><span class="sxs-lookup"><span data-stu-id="acfec-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="acfec-182">Пользователь с Интернет запросе страницы HTTP из hello общедоступный IP-адрес сетевого Адаптера, связанного с hello Сетевых IIS01 hello</span><span class="sxs-lookup"><span data-stu-id="acfec-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="acfec-183">Общедоступный IP-адрес Hello передает трафик toohello виртуальной сети к IIS01 (hello веб-сервера)</span><span class="sxs-lookup"><span data-stu-id="acfec-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="acfec-184">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="acfec-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="acfec-185">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="acfec-186">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="acfec-187">Применить правила NSG 3 (tooIIS01 Интернет), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="acfec-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="acfec-188">Трафик достигнет внутренний IP-адрес веб-сервера hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="acfec-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="acfec-189">IIS01 прослушивание веб-трафик, получает этот запрос и начинает обработку запроса hello</span><span class="sxs-lookup"><span data-stu-id="acfec-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="acfec-190">IIS01 запрашивает hello SQL Server на AppVM01 сведения</span><span class="sxs-lookup"><span data-stu-id="acfec-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="acfec-191">В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="acfec-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="acfec-192">подсети серверной Hello начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="acfec-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="acfec-193">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="acfec-194">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="acfec-195">Правила NSG 3 (Internet tooFirewall) не применяется, переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="acfec-196">Применить правила NSG 4 (IIS01 tooAppVM01), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="acfec-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="acfec-197">AppVM01 получает hello SQL-запрос и ответ</span><span class="sxs-lookup"><span data-stu-id="acfec-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="acfec-198">Поскольку имеются правила для исходящих подключений hello серверной подсети, может быть hello ответа</span><span class="sxs-lookup"><span data-stu-id="acfec-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="acfec-199">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="acfec-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="acfec-200">Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены</span><span class="sxs-lookup"><span data-stu-id="acfec-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="acfec-201">правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello.</span><span class="sxs-lookup"><span data-stu-id="acfec-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="acfec-202">Получает ответ SQL hello и завершения hello HTTP-ответ и отправляет инициатору запроса toohello Hello сервера IIS</span><span class="sxs-lookup"><span data-stu-id="acfec-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="acfec-203">Поскольку hello внешней подсети применяются правила для исходящих подключений, допускается ответа hello и hello пользователя Интернета получает hello веб-страницы, в запросе.</span><span class="sxs-lookup"><span data-stu-id="acfec-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="acfec-204">(*Разрешено*) tooIIS серверу удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="acfec-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="acfec-205">Является администратором сервера в Интернете запрашивает tooIIS01 сеанса протокола удаленного рабочего СТОЛА на hello общедоступный IP-адрес сетевого Адаптера, связанного с hello IIS01 сетевой Адаптер (это общедоступный IP-адрес может быть найден посредством hello портала или PowerShell) hello</span><span class="sxs-lookup"><span data-stu-id="acfec-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="acfec-206">Общедоступный IP-адрес Hello передает трафик toohello виртуальной сети к IIS01 (hello веб-сервера)</span><span class="sxs-lookup"><span data-stu-id="acfec-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="acfec-207">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="acfec-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="acfec-208">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="acfec-209">Правило 2 группы безопасности сети (RDP) применяется — трафик разрешается, дальнейшая обработка правил прекращается.</span><span class="sxs-lookup"><span data-stu-id="acfec-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="acfec-210">Правил для исходящего трафика нет, поэтому применяются правила по умолчанию и обратный трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="acfec-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="acfec-211">Начинается сеанс RDP.</span><span class="sxs-lookup"><span data-stu-id="acfec-211">RDP session is enabled</span></span>
6. <span data-ttu-id="acfec-212">Запрашивает IIS01 hello имя пользователя и пароль</span><span class="sxs-lookup"><span data-stu-id="acfec-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="acfec-213">tooRDP tooany серверы в этом экземпляре сервера IIS hello используется в качестве «переход поля».</span><span class="sxs-lookup"><span data-stu-id="acfec-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="acfec-214">Первый сервер IIS toohello RDP и затем с сервера hello серверной части toohello RDP сервера IIS.</span><span class="sxs-lookup"><span data-stu-id="acfec-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="acfec-215">DNS-запрос веб-сервера к серверу DNS (*разрешено*)</span><span class="sxs-lookup"><span data-stu-id="acfec-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="acfec-216">Веб-сервера, IIS01, потребности в www.data.gov, но потребности tooresolve hello адрес канала данных.</span><span class="sxs-lookup"><span data-stu-id="acfec-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="acfec-217">Hello конфигурацию сети для виртуальной сети hello списков DNS01 (10.0.2.4 подсети hello серверной части) как hello основной DNS-сервер, IIS01 отправляет запрос tooDNS01 hello DNS</span><span class="sxs-lookup"><span data-stu-id="acfec-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="acfec-218">В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="acfec-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="acfec-219">Подсеть BackEnd начинает обработку входящего правила:</span><span class="sxs-lookup"><span data-stu-id="acfec-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="acfec-220">Правило 1 группы безопасности сети (DNS) применяется — трафик разрешается, дальнейшая обработка правил прекращается.</span><span class="sxs-lookup"><span data-stu-id="acfec-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="acfec-221">DNS-сервер получает запрос hello</span><span class="sxs-lookup"><span data-stu-id="acfec-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="acfec-222">DNS-сервер не имеет адреса hello в кэше и запрашивает у корневой сервер DNS на hello Интернета</span><span class="sxs-lookup"><span data-stu-id="acfec-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="acfec-223">В подсети BackEnd нет правил для исходящего трафика, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="acfec-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="acfec-224">Internet DNS-сервер отвечает, поскольку этот сеанс был инициирован внутренне, допускается hello ответа</span><span class="sxs-lookup"><span data-stu-id="acfec-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="acfec-225">DNS-сервер кэширует ответ hello и реагирует назад tooIIS01 toohello исходного запроса</span><span class="sxs-lookup"><span data-stu-id="acfec-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="acfec-226">В подсети BackEnd нет правил для исходящего трафика, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="acfec-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="acfec-227">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="acfec-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="acfec-228">Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены</span><span class="sxs-lookup"><span data-stu-id="acfec-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="acfec-229">правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello</span><span class="sxs-lookup"><span data-stu-id="acfec-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="acfec-230">IIS01 получает hello ответа от DNS01</span><span class="sxs-lookup"><span data-stu-id="acfec-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="acfec-231">Обращение веб-сервера к файлу на сервере AppVM01 (*разрешено*)</span><span class="sxs-lookup"><span data-stu-id="acfec-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="acfec-232">IIS01 запрашивает файл на AppVM01</span><span class="sxs-lookup"><span data-stu-id="acfec-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="acfec-233">В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="acfec-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="acfec-234">подсети серверной Hello начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="acfec-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="acfec-235">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="acfec-236">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="acfec-237">Правила NSG 3 (Internet tooIIS01) не применяется, переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="acfec-238">Применить правила NSG 4 (IIS01 tooAppVM01), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="acfec-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="acfec-239">AppVM01 получает запрос hello и высылает файла (при условии, что права доступа)</span><span class="sxs-lookup"><span data-stu-id="acfec-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="acfec-240">Поскольку имеются правила для исходящих подключений hello серверной подсети, может быть hello ответа</span><span class="sxs-lookup"><span data-stu-id="acfec-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="acfec-241">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="acfec-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="acfec-242">Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены</span><span class="sxs-lookup"><span data-stu-id="acfec-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="acfec-243">правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello.</span><span class="sxs-lookup"><span data-stu-id="acfec-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="acfec-244">сервер IIS Hello получает файл hello</span><span class="sxs-lookup"><span data-stu-id="acfec-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="acfec-245">(*Отказано в доступе*) toobackend протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="acfec-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="acfec-246">Пользователь Интернета пытается tooRDP tooserver AppVM01</span><span class="sxs-lookup"><span data-stu-id="acfec-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="acfec-247">Так как существуют не общедоступные IP-адреса, связанные с этой серверы сетевого Адаптера, трафик будет не нужно вводить hello виртуальной сети и не достиг сервера hello</span><span class="sxs-lookup"><span data-stu-id="acfec-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="acfec-248">Однако если бы общедоступный IP-адрес был включен по какой-либо причине, правило 2 группы безопасности сети (RDP) разрешило бы прохождение этого трафика.</span><span class="sxs-lookup"><span data-stu-id="acfec-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="acfec-249">tooRDP tooany серверы в этом экземпляре сервера IIS hello используется в качестве «переход поля».</span><span class="sxs-lookup"><span data-stu-id="acfec-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="acfec-250">Первый сервер IIS toohello RDP и затем с сервера hello серверной части toohello RDP сервера IIS.</span><span class="sxs-lookup"><span data-stu-id="acfec-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="acfec-251">(*Отказано в доступе*) toobackend веб-сервера</span><span class="sxs-lookup"><span data-stu-id="acfec-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="acfec-252">Интернет-пользователь пытается tooaccess файл на AppVM01</span><span class="sxs-lookup"><span data-stu-id="acfec-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="acfec-253">Так как существуют не общедоступные IP-адреса, связанные с этой серверы сетевого Адаптера, трафик будет не нужно вводить hello виртуальной сети и не достиг сервера hello</span><span class="sxs-lookup"><span data-stu-id="acfec-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="acfec-254">Если по некоторым причинам было включено общедоступный IP-адрес, правило NSG 5 (Internet tooVNet) заблокирует этот трафик</span><span class="sxs-lookup"><span data-stu-id="acfec-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="acfec-255">DNS-запрос из Интернета к серверу DNS (*запрещено*)</span><span class="sxs-lookup"><span data-stu-id="acfec-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="acfec-256">Пользователь Интернета пытается toolook копирование DNS-запись внутренних на DNS01</span><span class="sxs-lookup"><span data-stu-id="acfec-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="acfec-257">Так как существуют не общедоступные IP-адреса, связанные с этой серверы сетевого Адаптера, трафик будет не нужно вводить hello виртуальной сети и не достиг сервера hello</span><span class="sxs-lookup"><span data-stu-id="acfec-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="acfec-258">Если по некоторым причинам было включено общедоступный IP-адрес, правило NSG 5 (Internet tooVNet) заблокирует этот трафик (Примечание:, правило 1 (DNS) не будут применяться, так как адрес источника запросы hello — hello Интернета и правила 1 относится только toohello виртуальной локальной сети как источник hello)</span><span class="sxs-lookup"><span data-stu-id="acfec-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="acfec-259">(*Отказано в доступе*) доступ к SQL на веб-сервере hello</span><span class="sxs-lookup"><span data-stu-id="acfec-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="acfec-260">Интернет-пользователь запрашивает данные SQL от сервера IIS01.</span><span class="sxs-lookup"><span data-stu-id="acfec-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="acfec-261">Так как существуют не общедоступные IP-адреса, связанные с этой серверы сетевого Адаптера, трафик будет не нужно вводить hello виртуальной сети и не достиг сервера hello</span><span class="sxs-lookup"><span data-stu-id="acfec-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="acfec-262">Если по некоторым причинам было включено общедоступный IP-адрес, hello внешней подсети начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="acfec-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="acfec-263">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="acfec-264">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="acfec-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="acfec-265">Применить правила NSG 3 (tooIIS01 Интернет), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="acfec-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="acfec-266">Трафик достигнет внутренний IP-адрес hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="acfec-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="acfec-267">IIS01 не прослушивает порт 1433, без запроса toohello ответа</span><span class="sxs-lookup"><span data-stu-id="acfec-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="acfec-268">Заключение</span><span class="sxs-lookup"><span data-stu-id="acfec-268">Conclusion</span></span>
<span data-ttu-id="acfec-269">В этом примере является относительно простой и простым способом изоляции hello внутренней подсети из входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="acfec-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="acfec-270">Дополнительные примеры и общие сведения о периметре безопасности сети можно найти [здесь][HOME].</span><span class="sxs-lookup"><span data-stu-id="acfec-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="acfec-271">Ссылки</span><span class="sxs-lookup"><span data-stu-id="acfec-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="acfec-272">Шаблон диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="acfec-272">Azure Resource Manager template</span></span>
<span data-ttu-id="acfec-273">В этом примере используется стандартный шаблон диспетчера ресурсов Azure в репозитории GitHub поддерживается корпорацией Майкрософт и откройте toohello сообщества.</span><span class="sxs-lookup"><span data-stu-id="acfec-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="acfec-274">Этот шаблон может развертываться из GitHub, или загружаются и изменить toofit вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="acfec-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="acfec-275">Hello главного шаблона находится в файле hello, с именем «azuredeploy.json.»</span><span class="sxs-lookup"><span data-stu-id="acfec-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="acfec-276">Этот шаблон могут передаваться через PowerShell или интерфейс командной строки (с файлом связанного» azuredeploy.parameters.json» hello) toodeploy этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="acfec-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="acfec-277">Найти hello простым способом является hello toouse кнопку «Развернуть tooAzure» на странице приветствия README.md в GitHub.</span><span class="sxs-lookup"><span data-stu-id="acfec-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="acfec-278">toodeploy hello шаблон, созданный в этом примере из GitHub и hello портал Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="acfec-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="acfec-279">В браузере перейдите toohello [шаблона][Template]</span><span class="sxs-lookup"><span data-stu-id="acfec-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="acfec-280">Щелкните кнопку «Развернуть tooAzure» hello (или toosee кнопку «Визуализировать» hello графическое представление этого шаблона)</span><span class="sxs-lookup"><span data-stu-id="acfec-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="acfec-281">Введите в колонке параметров hello hello учетной записи хранения, имя пользователя и пароль, затем щелкните **ОК**</span><span class="sxs-lookup"><span data-stu-id="acfec-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="acfec-282">Создайте группу ресурсов для этого развертывания (можно использовать существующую, но рекомендуется использовать новую для получения оптимальных результатов).</span><span class="sxs-lookup"><span data-stu-id="acfec-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="acfec-283">При необходимости измените параметры hello подписке и расположении для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="acfec-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="acfec-284">Нажмите кнопку **просмотрите условия**, ознакомьтесь с условиями hello и нажмите кнопку **покупки** tooagree.</span><span class="sxs-lookup"><span data-stu-id="acfec-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="acfec-285">Нажмите кнопку **создать** toobegin hello развертываний этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="acfec-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="acfec-286">После успешного завершения развертывания hello перейдите toohello создания для этого развертывания toosee hello ресурсов, настроенных в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="acfec-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="acfec-287">Этот шаблон позволяет RDP toohello IIS01 только сервер (hello поиска общедоступный IP-адрес для IIS01 на hello портала).</span><span class="sxs-lookup"><span data-stu-id="acfec-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="acfec-288">tooRDP tooany серверы в этом экземпляре сервера IIS hello используется в качестве «переход поля».</span><span class="sxs-lookup"><span data-stu-id="acfec-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="acfec-289">Первый сервер IIS toohello RDP и затем с сервера hello серверной части toohello RDP сервера IIS.</span><span class="sxs-lookup"><span data-stu-id="acfec-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="acfec-290">tooremove этого развертывания, hello удаления группы ресурсов и все дочерние ресурсы также будут удалены.</span><span class="sxs-lookup"><span data-stu-id="acfec-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="acfec-291">Примеры сценариев приложения</span><span class="sxs-lookup"><span data-stu-id="acfec-291">Sample application scripts</span></span>
<span data-ttu-id="acfec-292">После успешного выполнения шаблона hello настройкой hello веб-сервер и сервер приложений с простой web tooallow приложения, тестирование с помощью этой конфигурации сети Периметра.</span><span class="sxs-lookup"><span data-stu-id="acfec-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="acfec-293">tooinstall образец приложения для этого и других примерах DMZ, оно предоставлено в hello по ссылке: [образец приложения скрипта][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="acfec-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="acfec-294">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="acfec-294">Next steps</span></span>

* <span data-ttu-id="acfec-295">Разверните этот пример.</span><span class="sxs-lookup"><span data-stu-id="acfec-295">Deploy this example</span></span>
* <span data-ttu-id="acfec-296">Построение образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="acfec-296">Build hello sample application</span></span>
* <span data-ttu-id="acfec-297">Проверьте прохождение разных потоков трафика через эту сеть периметра.</span><span class="sxs-lookup"><span data-stu-id="acfec-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Входящая сеть периметра с группой безопасности сети"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md