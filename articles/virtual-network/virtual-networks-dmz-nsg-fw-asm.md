---
title: "Пример: aaaDMZ создавать DMZ tooprotect приложения с брандмауэром, Nsg | Документы Microsoft"
description: "Построение сети периметра с брандмауэром и группами безопасности сети"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="f40c8-103">Пример 2 — создавать DMZ tooprotect приложения с брандмауэром, Nsg</span><span class="sxs-lookup"><span data-stu-id="f40c8-103">Example 2 – Build a DMZ tooprotect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="f40c8-104">[Возвращает toohello страница лучшие рекомендации безопасности границ][HOME]</span><span class="sxs-lookup"><span data-stu-id="f40c8-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="f40c8-105">В этом примере будет создана сеть периметра с брандмауэром, четырьмя серверами Windows Server и группами безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="f40c8-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="f40c8-106">Он также поможет выполнить каждого из соответствующих команд tooprovide hello более глубокого понимания каждого шага.</span><span class="sxs-lookup"><span data-stu-id="f40c8-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="f40c8-107">Имеется также сценарий трафика раздел tooprovide на подробные пошаговые трафик проходит через hello уровней защиты в hello DMZ.</span><span class="sxs-lookup"><span data-stu-id="f40c8-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="f40c8-108">Наконец, в разделе references hello hello полный код и должна toobuild инструкция этот tootest среды и эксперимента с помощью различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="f40c8-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="f40c8-109">![Входящий DMZ с Уязвимости и NSG][1]</span><span class="sxs-lookup"><span data-stu-id="f40c8-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="f40c8-110">Описание среды</span><span class="sxs-lookup"><span data-stu-id="f40c8-110">Environment Description</span></span>
<span data-ttu-id="f40c8-111">В этом примере имеется подписка, содержащий hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f40c8-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="f40c8-112">две облачные службы: FrontEnd001 и BackEnd001;</span><span class="sxs-lookup"><span data-stu-id="f40c8-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="f40c8-113">виртуальная сеть CorpNetwork с двумя подсетями (FrontEnd и BackEnd);</span><span class="sxs-lookup"><span data-stu-id="f40c8-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="f40c8-114">Одну группу безопасности сети, будет применен tooboth подсети</span><span class="sxs-lookup"><span data-stu-id="f40c8-114">A single Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="f40c8-115">Устройство виртуальной сети, в этом примере брандмауэр Barracuda NextGen, подключен toohello внешней подсети</span><span class="sxs-lookup"><span data-stu-id="f40c8-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected toohello Frontend subnet</span></span>
* <span data-ttu-id="f40c8-116">сервер Windows Server, который представляет веб-сервер приложений (IIS01);</span><span class="sxs-lookup"><span data-stu-id="f40c8-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="f40c8-117">два сервера Windows Server, представляющих тыловые серверы приложений (AppVM01, AppVM02);</span><span class="sxs-lookup"><span data-stu-id="f40c8-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="f40c8-118">сервер Windows Server, который представляет DNS-сервер (DNS01).</span><span class="sxs-lookup"><span data-stu-id="f40c8-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="f40c8-119">Несмотря на то, что в этом примере используется брандмауэр Barracuda NextGen, многие из разных виртуальных сетевых устройств, которые могут использоваться в этом примере приветствия.</span><span class="sxs-lookup"><span data-stu-id="f40c8-119">Although this example uses a Barracuda NextGen Firewall, many of hello different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="f40c8-120">В разделе references hello ниже имеется сценарий PowerShell, построит большая часть среды hello, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="f40c8-120">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="f40c8-121">Построение hello ВМ и виртуальными сетями, несмотря на то, что может быть выполнено с hello пример скрипта, не подробно описаны в этом документе.</span><span class="sxs-lookup"><span data-stu-id="f40c8-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="f40c8-122">Среда toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="f40c8-122">toobuild hello environment:</span></span>

1. <span data-ttu-id="f40c8-123">Сохраните hello сетевой конфигурации XML-файл включаются в раздел ссылок hello (обновлено с именами, расположение и toomatch hello заданному IP адресов сценарий)</span><span class="sxs-lookup"><span data-stu-id="f40c8-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="f40c8-124">Переменные пользователя hello обновления в скрипт hello среды hello toomatch hello скрипта является toobe выполняться (подписок, имена служб, и т. д.)</span><span class="sxs-lookup"><span data-stu-id="f40c8-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="f40c8-125">Выполните сценарий hello в PowerShell</span><span class="sxs-lookup"><span data-stu-id="f40c8-125">Execute hello script in PowerShell</span></span>

<span data-ttu-id="f40c8-126">**Примечание**: hello область — в hello сценарий PowerShell должен соответствовать hello область — в XML-файл конфигурации сети hello.</span><span class="sxs-lookup"><span data-stu-id="f40c8-126">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="f40c8-127">После успешного выполнения сценария hello может быть переведена hello следующие шаги после сценария:</span><span class="sxs-lookup"><span data-stu-id="f40c8-127">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="f40c8-128">Настройка правил брандмауэра hello, это рассматривается в hello ниже раздел: правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="f40c8-128">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="f40c8-129">При необходимости в разделе references hello являются двумя tooset сценарии hello веб-сервер и сервер приложений с простой web tooallow приложения, тестирование с помощью этой конфигурации сети Периметра.</span><span class="sxs-lookup"><span data-stu-id="f40c8-129">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="f40c8-130">Hello следующем разделе показано большинство hello сценарии операторы относительных tooNetwork групп безопасности.</span><span class="sxs-lookup"><span data-stu-id="f40c8-130">hello next section explains most of hello scripts statements relative tooNetwork Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="f40c8-131">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="f40c8-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="f40c8-132">В этом примере создается группа безопасности сети, после чего в нее загружаются шесть правил.</span><span class="sxs-lookup"><span data-stu-id="f40c8-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="f40c8-133">Вообще говоря следует сначала создать определенные правила «Разрешить», а затем последнего hello более универсальный правила «Deny».</span><span class="sxs-lookup"><span data-stu-id="f40c8-133">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="f40c8-134">Привет, назначается приоритет, определяет, какие правила вычисляются первыми.</span><span class="sxs-lookup"><span data-stu-id="f40c8-134">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="f40c8-135">После обнаружения tooapply tooa конкретного правила трафика вычисляются другим правилам.</span><span class="sxs-lookup"><span data-stu-id="f40c8-135">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="f40c8-136">Правила NSG можно применить в любом в hello входящего и исходящего направления (с точки зрения hello hello подсети).</span><span class="sxs-lookup"><span data-stu-id="f40c8-136">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="f40c8-137">Создаются декларативно, hello следующие правила для входящего трафика:</span><span class="sxs-lookup"><span data-stu-id="f40c8-137">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="f40c8-138">Внутренний трафик DNS (порт 53) разрешается.</span><span class="sxs-lookup"><span data-stu-id="f40c8-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="f40c8-139">RDP (порт 3389) из tooany Интернет hello VM-трафика</span><span class="sxs-lookup"><span data-stu-id="f40c8-139">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="f40c8-140">Может быть HTTP-трафика (порт 80) из Интернета hello toohello NVA (брандмауэром)</span><span class="sxs-lookup"><span data-stu-id="f40c8-140">HTTP traffic (port 80) from hello Internet toohello NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="f40c8-141">Все (все порты) из IIS01 tooAppVM1-трафика</span><span class="sxs-lookup"><span data-stu-id="f40c8-141">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="f40c8-142">Любой трафик (все порты) из Интернета toohello hello запрещен всей виртуальной сети (оба подсети)</span><span class="sxs-lookup"><span data-stu-id="f40c8-142">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="f40c8-143">Любой трафик (все порты) из hello внешней подсети toohello серверной подсети запрещен</span><span class="sxs-lookup"><span data-stu-id="f40c8-143">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="f40c8-144">С подсетью привязанного tooeach эти правила, если входящие данные от hello Internet toohello веб-сервера HTTP-запроса оба правила 3 (Разрешить) и 5 (запретить) будет применен, но поскольку правило 3 обладает более высоким приоритетом только он будет применен и правила 5 бы не следует учитывать.</span><span class="sxs-lookup"><span data-stu-id="f40c8-144">With these rules bound tooeach subnet, if a HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="f40c8-145">Таким образом запрос hello HTTP допустимы toohello брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="f40c8-145">Thus hello HTTP request would be allowed toohello firewall.</span></span> <span data-ttu-id="f40c8-146">Если же трафик осуществлялось tooreach hello DNS01 server, правило 5 (Deny) бы бы hello первый tooapply и hello трафик не будет разрешен toopass toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="f40c8-146">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="f40c8-147">Правила 6 внешней подсети hello (Deny) блоки из взаимодействии подсети серверной toohello (за исключением разрешенного трафика в правилах 1 и 4), это позволяет защитить hello серверной сети, если злоумышленник взломает hello веб-приложения на hello переднего плана, hello злоумышленник ограниченный доступ toohello серверной» защищенной» (только tooresources, предоставляемые на сервере AppVM01 hello).</span><span class="sxs-lookup"><span data-stu-id="f40c8-147">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="f40c8-148">Имеется по умолчанию правило исходящего трафика, которое разрешает трафик, исходящий toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="f40c8-148">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="f40c8-149">В этом примере мы разрешаем исходящий трафик и не меняем никаких исходящих правил.</span><span class="sxs-lookup"><span data-stu-id="f40c8-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="f40c8-150">toolock трафик в обоих направлениях маршрутизации определенные пользователя не требуется, это изучена в другой пример, в котором можно найти в hello [документа границ безопасности основного][HOME].</span><span class="sxs-lookup"><span data-stu-id="f40c8-150">toolock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in hello [main security boundary document][HOME].</span></span>

<span data-ttu-id="f40c8-151">описанные выше Hello правила NSG являются очень схожие правила NSG toohello в [пример 1 - построение простого DMZ с Nsg][Example1].</span><span class="sxs-lookup"><span data-stu-id="f40c8-151">hello above discussed NSG rules are very similar toohello NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="f40c8-152">Просмотрите hello NSG описание в этом документе для подробное описание каждого правила NSG и его атрибуты.</span><span class="sxs-lookup"><span data-stu-id="f40c8-152">Please review hello NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="f40c8-153">Правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="f40c8-153">Firewall Rules</span></span>
<span data-ttu-id="f40c8-154">Клиент управления будет требуется toobe установлен брандмауэр hello toomanage ПК и создавать hello конфигурациях.</span><span class="sxs-lookup"><span data-stu-id="f40c8-154">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="f40c8-155">См. документации из брандмауэр (или другие Уязвимости) поставщика hello как toomanage hello устройства.</span><span class="sxs-lookup"><span data-stu-id="f40c8-155">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="f40c8-156">Hello оставшейся части данного раздела описывается hello конфигурации брандмауэра hello, через hello клиент управления поставщиков (т. е. не hello портал Azure или PowerShell).</span><span class="sxs-lookup"><span data-stu-id="f40c8-156">hello remainder of this section will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="f40c8-157">Инструкции по загрузки клиента и подключении toohello Barracuda используется в этом примере можно найти здесь: [Barracuda NG администратора](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="f40c8-157">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="f40c8-158">На брандмауэре hello правила перенаправления потребуется создать toobe.</span><span class="sxs-lookup"><span data-stu-id="f40c8-158">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="f40c8-159">Так как в этом примере только направляет трафик входящих toohello при использовании брандмауэра, а затем toohello веб-сервера, пересылки только одно правило NAT необходим.</span><span class="sxs-lookup"><span data-stu-id="f40c8-159">Since this example only routes internet traffic in-bound toohello firewall and then toohello web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="f40c8-160">На hello брандмауэр Barracuda NextGen, используемых в этом примере hello правило будет NAT назначения правила toopass («Dst NAT») этого трафика.</span><span class="sxs-lookup"><span data-stu-id="f40c8-160">On hello Barracuda NextGen Firewall used in this example hello rule would be a Destination NAT rule (“Dst NAT”) toopass this traffic.</span></span>

<span data-ttu-id="f40c8-161">toocreate hello следующих правил (или проверить существующие правила по умолчанию), начиная с панели мониторинга клиент Barracuda NG Admin hello, перейдите на вкладку Конфигурация toohello, в hello рабочей конфигурации нажмите кнопку набора правил.</span><span class="sxs-lookup"><span data-stu-id="f40c8-161">toocreate hello following rule (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="f40c8-162">Вызывается сетку, «Main правила» будет отображаться hello существующие активные и неактивные правила брандмауэра hello.</span><span class="sxs-lookup"><span data-stu-id="f40c8-162">A grid called, “Main Rules” will show hello existing active and deactivated rules on hello firewall.</span></span> <span data-ttu-id="f40c8-163">Верхний правый угол hello сетки является небольшой, зеленый «+», выберите элемент этого toocreate новое правило (Примечание: брандмауэра «заблокирована» для изменения, если помечены кнопки «Блокировка» и, не удается toocreate или изменение правил, нажмите кнопку эта кнопка слишком «разблокировать» hello набор правил и разрешить изменение).</span><span class="sxs-lookup"><span data-stu-id="f40c8-163">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello ruleset and allow editing).</span></span> <span data-ttu-id="f40c8-164">При желании tooedit существующее правило, выберите это правило, щелкните правой кнопкой мыши и выберите команду Изменить правило.</span><span class="sxs-lookup"><span data-stu-id="f40c8-164">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="f40c8-165">Создайте новое правило и укажите имя правила, например WebTraffic.</span><span class="sxs-lookup"><span data-stu-id="f40c8-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="f40c8-166">значок правила NAT назначения Hello выглядит следующим образом: ![NAT значок назначения][2]</span><span class="sxs-lookup"><span data-stu-id="f40c8-166">hello Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="f40c8-167">само правило Hello будет выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f40c8-167">hello rule itself would look something like this:</span></span>

<span data-ttu-id="f40c8-168">![Правила брандмауэра][3]</span><span class="sxs-lookup"><span data-stu-id="f40c8-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="f40c8-169">Здесь адреса входящего трафика, что попаданий hello брандмауэра попытки tooreach HTTP (порт 80 или 443 для HTTPS) будут отправлены Здравствуйте, «Локальные DHCP1 IP-адрес» интерфейс и перенаправленный toohello веб-сервер с IP-адрес 10.0.1.5 hello брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="f40c8-169">Here any inbound address that hits hello Firewall trying tooreach HTTP (port 80 or 443 for HTTPS) will be sent out hello Firewall’s “DHCP1 Local IP” interface and redirected toohello Web Server with hello IP Address of 10.0.1.5.</span></span> <span data-ttu-id="f40c8-170">Поскольку hello трафик поступает порт 80 и постоянной toohello веб-сервера на порт 80 без изменений порт не требовались.</span><span class="sxs-lookup"><span data-stu-id="f40c8-170">Since hello traffic is coming in on port 80 and going toohello web server on port 80 no port change was needed.</span></span> <span data-ttu-id="f40c8-171">Тем не менее целевой список были бы 10.0.1.5:8080 Если веб-сервере прослушивал порт 8080 таким образом выполнении приветствия hello входящий порт 80 hello брандмауэра tooinbound порт 8080 hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="f40c8-171">However, hello Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating hello inbound port 80 on hello firewall tooinbound port 8080 on hello web server.</span></span>

<span data-ttu-id="f40c8-172">Метод подключения должны также быть обозначать, для hello правила назначения из Интернета, hello «Динамического SNAT» лучше всего подходит.</span><span class="sxs-lookup"><span data-stu-id="f40c8-172">A Connection Method should also be signified, for hello Destination Rule from hello Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="f40c8-173">Несмотря на то что было создано только одно правило, важно правильно задать его приоритет.</span><span class="sxs-lookup"><span data-stu-id="f40c8-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="f40c8-174">Если в сетке hello всех правил в брандмауэре hello это новое правило нижней hello (см. ниже правило «BLOCKALL» hello) никогда не перейдет в игру.</span><span class="sxs-lookup"><span data-stu-id="f40c8-174">If in hello grid of all rules on hello firewall this new rule is on hello bottom (below hello "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="f40c8-175">Убедитесь, что выше правила BLOCKALL hello hello вновь созданные правила для веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="f40c8-175">Ensure hello newly created rule for web traffic is above hello BLOCKALL rule.</span></span>

<span data-ttu-id="f40c8-176">После создания правила hello, он должен быть принудительно отправлены toohello брандмауэра и затем активируется, если этого не сделать hello правило, изменения не вступят в силу.</span><span class="sxs-lookup"><span data-stu-id="f40c8-176">Once hello rule is created, it must be pushed toohello firewall and then activated, if this is not done hello rule change will not take effect.</span></span> <span data-ttu-id="f40c8-177">Hello принудительной отправки и активации процесс описан в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="f40c8-177">hello push and activation process is described in hello next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="f40c8-178">Активация правил</span><span class="sxs-lookup"><span data-stu-id="f40c8-178">Rule Activation</span></span>
<span data-ttu-id="f40c8-179">С hello ruleset изменен tooadd это правило, hello ruleset должен быть отправлен toohello брандмауэра и активации.</span><span class="sxs-lookup"><span data-stu-id="f40c8-179">With hello ruleset modified tooadd this rule, hello ruleset must be uploaded toohello firewall and activated.</span></span>

<span data-ttu-id="f40c8-180">![Активация правила брандмауэра][4]</span><span class="sxs-lookup"><span data-stu-id="f40c8-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="f40c8-181">В правом верхнем углу hello клиент управления hello являются кластера кнопок.</span><span class="sxs-lookup"><span data-stu-id="f40c8-181">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="f40c8-182">Щелкните toohello «Изменения отправить «hello кнопка toosend hello изменены правила брандмауэра, а затем нажмите кнопку «Активировать» hello.</span><span class="sxs-lookup"><span data-stu-id="f40c8-182">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="f40c8-183">Hello активации из набора правил брандмауэра hello с этой сборкой среды пример завершена.</span><span class="sxs-lookup"><span data-stu-id="f40c8-183">With hello activation of hello firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="f40c8-184">При необходимости скрипты сборки hello post в hello ссылки на раздел может быть запустите tooadd среды tootest приложения toothis hello ниже сценарии трафика.</span><span class="sxs-lookup"><span data-stu-id="f40c8-184">Optionally, hello post build scripts in hello References section can be run tooadd an application toothis environment tootest hello below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f40c8-185">Это критическое toorealize, что вы не столкнутся hello веб-сервер напрямую.</span><span class="sxs-lookup"><span data-stu-id="f40c8-185">It is critical toorealize that you will not hit hello web server directly.</span></span> <span data-ttu-id="f40c8-186">Когда браузер запрашивает страницу HTTP из FrontEnd001.CloudApp.Net, hello HTTP (порт 80) конечная точка передает этот брандмауэр toohello трафик не hello веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="f40c8-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, hello HTTP endpoint (port 80) passes this traffic toohello firewall not hello web server.</span></span> <span data-ttu-id="f40c8-187">Здравствуйте брандмауэра, затем toohello правила в соответствии с созданным ранее, NAT, запрашивающих toohello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="f40c8-187">hello firewall then, according toohello rule created above, NATs that request toohello Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="f40c8-188">Варианты прохождения трафика</span><span class="sxs-lookup"><span data-stu-id="f40c8-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-tooweb-server-through-firewall"></a><span data-ttu-id="f40c8-189">(Разрешено) TooWeb Web Server через брандмауэр</span><span class="sxs-lookup"><span data-stu-id="f40c8-189">(Allowed) Web tooWeb Server through Firewall</span></span>
1. <span data-ttu-id="f40c8-190">Интернет-пользователь запрашивает страницу HTTP из FrontEnd001.CloudApp.Net (облачная служба, открытая для доступа через Интернет)</span><span class="sxs-lookup"><span data-stu-id="f40c8-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="f40c8-191">Облачные службы передает трафик через открытую конечную точку в локальном интерфейсе toofirewall порт 80 на 10.0.1.4:80</span><span class="sxs-lookup"><span data-stu-id="f40c8-191">Cloud service passes traffic through open endpoint on port 80 toofirewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="f40c8-192">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="f40c8-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f40c8-193">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f40c8-194">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="f40c8-195">Применить правила NSG 3 (tooFirewall Интернет), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="f40c8-195">NSG Rule 3 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="f40c8-196">Трафик достигнет внутренний IP-адрес брандмауэра hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="f40c8-196">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="f40c8-197">Правило пересылки брандмауэра см. это трафик на порт 80, происходит его перенаправление веб-сервере toohello IIS01</span><span class="sxs-lookup"><span data-stu-id="f40c8-197">Firewall forwarding rule see this is port 80 traffic, redirects it toohello web server IIS01</span></span>
6. <span data-ttu-id="f40c8-198">IIS01 прослушивание веб-трафик, получает этот запрос и начинает обработку запроса hello</span><span class="sxs-lookup"><span data-stu-id="f40c8-198">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
7. <span data-ttu-id="f40c8-199">IIS01 запрашивает hello SQL Server на AppVM01 сведения</span><span class="sxs-lookup"><span data-stu-id="f40c8-199">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="f40c8-200">В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="f40c8-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="f40c8-201">подсети серверной Hello начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="f40c8-201">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f40c8-202">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-202">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f40c8-203">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-203">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="f40c8-204">Правила NSG 3 (Internet tooFirewall) не применяется, переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-204">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="f40c8-205">Применить правила NSG 4 (IIS01 tooAppVM01), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="f40c8-205">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="f40c8-206">AppVM01 получает hello SQL-запрос и ответ</span><span class="sxs-lookup"><span data-stu-id="f40c8-206">AppVM01 receives hello SQL Query and responds</span></span>
11. <span data-ttu-id="f40c8-207">Так как имеются может быть не правила для исходящих подключений на hello ответа hello подсети серверной части</span><span class="sxs-lookup"><span data-stu-id="f40c8-207">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
12. <span data-ttu-id="f40c8-208">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="f40c8-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f40c8-209">Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены</span><span class="sxs-lookup"><span data-stu-id="f40c8-209">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="f40c8-210">правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello.</span><span class="sxs-lookup"><span data-stu-id="f40c8-210">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
13. <span data-ttu-id="f40c8-211">Получает ответ SQL hello и завершения hello HTTP-ответ и отправляет запрашивающей стороны toohello Hello сервера IIS</span><span class="sxs-lookup"><span data-stu-id="f40c8-211">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
14. <span data-ttu-id="f40c8-212">Поскольку это сеанс NAT из брандмауэра hello, назначение ответа hello (первоначально) — для hello брандмауэра</span><span class="sxs-lookup"><span data-stu-id="f40c8-212">Since this is a NAT session from hello firewall, hello response destination (initially) is for hello Firewall</span></span>
15. <span data-ttu-id="f40c8-213">брандмауэр Hello получает hello ответа от hello веб-сервера и пересылает задней toohello пользователя Интернета</span><span class="sxs-lookup"><span data-stu-id="f40c8-213">hello firewall receives hello response from hello Web Server and forwards back toohello Internet User</span></span>
16. <span data-ttu-id="f40c8-214">Так как имеются исходящего правила на hello интерфейсной подсети hello ответа не допускается, и hello пользователя Интернета получает hello веб-страницы, в запросе.</span><span class="sxs-lookup"><span data-stu-id="f40c8-214">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="f40c8-215">(Разрешено) TooBackend протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="f40c8-215">(Allowed) RDP tooBackend</span></span>
1. <span data-ttu-id="f40c8-216">Администратор сервера в Интернете запрашивает tooAppVM01 сеанс RDP в BackEnd001.CloudApp.Net:xxxxx, где xxxxx-hello случайным образом назначенный номер порта для протокола удаленного рабочего СТОЛА tooAppVM01 (hello назначенный порт можно найти на портале Azure hello или с помощью PowerShell)</span><span class="sxs-lookup"><span data-stu-id="f40c8-216">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="f40c8-217">С момента hello, брандмауэр только прослушивание hello FrontEnd001.CloudApp.Net адрес он не участвует в этот поток трафика</span><span class="sxs-lookup"><span data-stu-id="f40c8-217">Since hello Firewall is only listening on hello FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="f40c8-218">Подсеть BackEnd начинает обработку правила для входящего трафика:</span><span class="sxs-lookup"><span data-stu-id="f40c8-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f40c8-219">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-219">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f40c8-220">Правило 2 группы безопасности сети (RDP) применяется — трафик разрешается, дальнейшая обработка правил прекращается.</span><span class="sxs-lookup"><span data-stu-id="f40c8-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="f40c8-221">Правил для исходящего трафика нет, поэтому применяются правила по умолчанию и обратный трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="f40c8-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="f40c8-222">Начинается сеанс RDP.</span><span class="sxs-lookup"><span data-stu-id="f40c8-222">RDP session is enabled</span></span>
6. <span data-ttu-id="f40c8-223">Сервер AppVM01 запрашивает имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="f40c8-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="f40c8-224">DNS-запрос веб-сервера к серверу DNS (разрешено) </span><span class="sxs-lookup"><span data-stu-id="f40c8-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="f40c8-225">Веб-сервера, IIS01, потребности в www.data.gov, но потребности tooresolve hello адрес канала данных.</span><span class="sxs-lookup"><span data-stu-id="f40c8-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="f40c8-226">Hello конфигурацию сети для виртуальной сети hello списков DNS01 (10.0.2.4 подсети hello серверной части) как hello основной DNS-сервер, IIS01 отправляет запрос tooDNS01 hello DNS</span><span class="sxs-lookup"><span data-stu-id="f40c8-226">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="f40c8-227">В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="f40c8-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="f40c8-228">Подсеть BackEnd начинает обработку входящего правила:</span><span class="sxs-lookup"><span data-stu-id="f40c8-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f40c8-229">Правило 1 группы безопасности сети (DNS) применяется — трафик разрешается, дальнейшая обработка правил прекращается.</span><span class="sxs-lookup"><span data-stu-id="f40c8-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="f40c8-230">DNS-сервер получает запрос hello</span><span class="sxs-lookup"><span data-stu-id="f40c8-230">DNS server receives hello request</span></span>
6. <span data-ttu-id="f40c8-231">DNS-сервер не имеет адреса hello в кэше и запрашивает у корневой сервер DNS на hello Интернета</span><span class="sxs-lookup"><span data-stu-id="f40c8-231">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="f40c8-232">В подсети BackEnd нет правил для исходящего трафика, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="f40c8-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="f40c8-233">Internet DNS-сервер отвечает, поскольку этот сеанс был инициирован внутренне, допускается hello ответа</span><span class="sxs-lookup"><span data-stu-id="f40c8-233">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="f40c8-234">DNS-сервер кэширует ответ hello и реагирует назад tooIIS01 toohello исходного запроса</span><span class="sxs-lookup"><span data-stu-id="f40c8-234">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="f40c8-235">В подсети BackEnd нет правил для исходящего трафика, поэтому трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="f40c8-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="f40c8-236">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="f40c8-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f40c8-237">Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены</span><span class="sxs-lookup"><span data-stu-id="f40c8-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="f40c8-238">правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello</span><span class="sxs-lookup"><span data-stu-id="f40c8-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="f40c8-239">IIS01 получает hello ответа от DNS01</span><span class="sxs-lookup"><span data-stu-id="f40c8-239">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="f40c8-240">(Разрешено) Веб-сервер обращается к файлу на AppVM01</span><span class="sxs-lookup"><span data-stu-id="f40c8-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="f40c8-241">IIS01 запрашивает файл на AppVM01</span><span class="sxs-lookup"><span data-stu-id="f40c8-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="f40c8-242">В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.</span><span class="sxs-lookup"><span data-stu-id="f40c8-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="f40c8-243">подсети серверной Hello начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="f40c8-243">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f40c8-244">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-244">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f40c8-245">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-245">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="f40c8-246">Правила NSG 3 (Internet tooFirewall) не применяется, переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-246">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="f40c8-247">Применить правила NSG 4 (IIS01 tooAppVM01), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="f40c8-247">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="f40c8-248">AppVM01 получает запрос hello и высылает файла (при условии, что права доступа)</span><span class="sxs-lookup"><span data-stu-id="f40c8-248">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="f40c8-249">Так как имеются может быть не правила для исходящих подключений на hello ответа hello подсети серверной части</span><span class="sxs-lookup"><span data-stu-id="f40c8-249">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
6. <span data-ttu-id="f40c8-250">Подсеть Frontend начинает обработку правила для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="f40c8-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f40c8-251">Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены</span><span class="sxs-lookup"><span data-stu-id="f40c8-251">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="f40c8-252">правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello.</span><span class="sxs-lookup"><span data-stu-id="f40c8-252">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="f40c8-253">сервер IIS Hello получает файл hello</span><span class="sxs-lookup"><span data-stu-id="f40c8-253">hello IIS server receives hello file</span></span>

#### <a name="denied-web-direct-tooweb-server"></a><span data-ttu-id="f40c8-254">(Запрещено) Прямой tooWeb Web Server</span><span class="sxs-lookup"><span data-stu-id="f40c8-254">(Denied) Web direct tooWeb Server</span></span>
<span data-ttu-id="f40c8-255">С момента hello веб-сервера, IIS01 и hello брандмауэра в hello одной облачной службе, они совместно используют hello же открытый IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="f40c8-255">Since hello Web Server, IIS01, and hello Firewall are in hello same Cloud Service they share hello same public facing IP address.</span></span> <span data-ttu-id="f40c8-256">Таким образом будет направляться трафик HTTP toohello брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="f40c8-256">Thus any HTTP traffic would be directed toohello firewall.</span></span> <span data-ttu-id="f40c8-257">Хотя бы успешно предоставил hello запроса, не может ссылаться непосредственно toohello веб-сервера, он прошел, как было задумано, сначала через hello брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="f40c8-257">While hello request would be successfully served, it cannot go directly toohello Web Server, it passed, as designed, through hello Firewall first.</span></span> <span data-ttu-id="f40c8-258">В разделе hello первый сценарий в этом разделе для потока трафика hello.</span><span class="sxs-lookup"><span data-stu-id="f40c8-258">See hello first Scenario in this section for hello traffic flow.</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="f40c8-259">(Запрещено) Веб-сервера tooBackend</span><span class="sxs-lookup"><span data-stu-id="f40c8-259">(Denied) Web tooBackend Server</span></span>
1. <span data-ttu-id="f40c8-260">Пользователь Интернета пытается tooaccess файл на AppVM01 через hello BackEnd001.CloudApp.Net службы</span><span class="sxs-lookup"><span data-stu-id="f40c8-260">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="f40c8-261">Поскольку конечные точки не открыты для общего файлового ресурса, это не будет передан hello облачной службы и не достигают сервера hello</span><span class="sxs-lookup"><span data-stu-id="f40c8-261">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="f40c8-262">Если по некоторым причинам hello конечные точки были открыты, правило NSG 5 (Internet tooVNet) заблокирует этот трафик</span><span class="sxs-lookup"><span data-stu-id="f40c8-262">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="f40c8-263">(Запрещено) DNS-запрос из Интернета к серверу DNS</span><span class="sxs-lookup"><span data-stu-id="f40c8-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="f40c8-264">Пользователь Интернета пытается toolookup внутренние DNS-запись на DNS01 через hello BackEnd001.CloudApp.Net службы</span><span class="sxs-lookup"><span data-stu-id="f40c8-264">Internet user tries toolookup an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="f40c8-265">Поскольку конечные точки не открыты для DNS, это не будет передан hello облачной службы и не достигают сервера hello</span><span class="sxs-lookup"><span data-stu-id="f40c8-265">Since there are no endpoints open for DNS, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="f40c8-266">Если по некоторым причинам hello конечные точки были открыты, правило NSG 5 (Internet tooVNet) заблокирует этот трафик (Примечание: 1 правило (DNS) не будут применяться по двум причинам, исходный адрес первого hello hello Интернета, это правило применяется только toohello также виртуальной локальной сети как hello источника Это правило разрешить, поэтому она никогда не будет запрещать трафик)</span><span class="sxs-lookup"><span data-stu-id="f40c8-266">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="f40c8-267">(Запрещено) Веб-tooSQL доступ через брандмауэр</span><span class="sxs-lookup"><span data-stu-id="f40c8-267">(Denied) Web tooSQL access through Firewall</span></span>
1. <span data-ttu-id="f40c8-268">Интернет-пользователь данные SQL из FrontEnd001.CloudApp.Net (облачная служба, открытая для доступа через Интернет)</span><span class="sxs-lookup"><span data-stu-id="f40c8-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="f40c8-269">Поскольку конечные точки не открыты для SQL, это не будет передан hello облачной службы и не будет достигнут hello брандмауэра</span><span class="sxs-lookup"><span data-stu-id="f40c8-269">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="f40c8-270">Если конечные точки были открыты для какой-либо причине, hello внешней подсети начинает обработку входящее правило:</span><span class="sxs-lookup"><span data-stu-id="f40c8-270">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f40c8-271">Не применяется правило 1 NSG (DNS), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-271">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="f40c8-272">Не применяется правило 2 NSG (RDP), переместите toonext правило</span><span class="sxs-lookup"><span data-stu-id="f40c8-272">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="f40c8-273">Применить правило NSG 2 (Internet tooFirewall), будет разрешен, остановите правила обработки трафика</span><span class="sxs-lookup"><span data-stu-id="f40c8-273">NSG Rule 2 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="f40c8-274">Трафик достигнет внутренний IP-адрес брандмауэра hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="f40c8-274">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="f40c8-275">Нет правила перенаправления имеет брандмауэр для SQL и удаляет hello трафика</span><span class="sxs-lookup"><span data-stu-id="f40c8-275">Firewall has no forwarding rules for SQL and drops hello traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="f40c8-276">Заключение</span><span class="sxs-lookup"><span data-stu-id="f40c8-276">Conclusion</span></span>
<span data-ttu-id="f40c8-277">Этот способ относительно прост для защиты приложения с брандмауэром и изоляции hello серверной части подсети из входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="f40c8-277">This is a relatively straight forward way of protecting your application with a firewall and isolating hello back end subnet from inbound traffic.</span></span>

<span data-ttu-id="f40c8-278">Дополнительные примеры и общие сведения о периметре безопасности сети можно найти [здесь][HOME].</span><span class="sxs-lookup"><span data-stu-id="f40c8-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="f40c8-279">Ссылки</span><span class="sxs-lookup"><span data-stu-id="f40c8-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="f40c8-280">Основной сценарий и конфигурация сети</span><span class="sxs-lookup"><span data-stu-id="f40c8-280">Main Script and Network Config</span></span>
<span data-ttu-id="f40c8-281">Сохраните hello полный скрипт в файл скрипта PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f40c8-281">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="f40c8-282">Сохраните hello сетевой конфигурации в файл с именем «NetworkConf2.xml».</span><span class="sxs-lookup"><span data-stu-id="f40c8-282">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="f40c8-283">При необходимости измените hello определенные пользователем переменные.</span><span class="sxs-lookup"><span data-stu-id="f40c8-283">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="f40c8-284">Запустите сценарий hello, а затем выполните hello брандмауэра правила установки инструкции выше.</span><span class="sxs-lookup"><span data-stu-id="f40c8-284">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="f40c8-285">Полный сценарий</span><span class="sxs-lookup"><span data-stu-id="f40c8-285">Full Script</span></span>
<span data-ttu-id="f40c8-286">Этот скрипт будет, на основе hello определяемых пользователем переменных:</span><span class="sxs-lookup"><span data-stu-id="f40c8-286">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="f40c8-287">Подключение tooan подписки Azure</span><span class="sxs-lookup"><span data-stu-id="f40c8-287">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="f40c8-288">Создание новой учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="f40c8-288">Create a new storage account</span></span>
3. <span data-ttu-id="f40c8-289">Создайте новую виртуальную сеть и две подсети, как определено в файле конфигурации сети hello</span><span class="sxs-lookup"><span data-stu-id="f40c8-289">Create a new VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="f40c8-290">Создаст четыре виртуальные машины под управлением Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f40c8-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="f40c8-291">Настроит группу безопасности сети:</span><span class="sxs-lookup"><span data-stu-id="f40c8-291">Configure NSG including:</span></span>
   * <span data-ttu-id="f40c8-292">создаст группу безопасности сети;</span><span class="sxs-lookup"><span data-stu-id="f40c8-292">Creating a NSG</span></span>
   * <span data-ttu-id="f40c8-293">добавит в нее правила;</span><span class="sxs-lookup"><span data-stu-id="f40c8-293">Populating it with rules</span></span>
   * <span data-ttu-id="f40c8-294">Привязка hello NSG toohello соответствующие подсети</span><span class="sxs-lookup"><span data-stu-id="f40c8-294">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="f40c8-295">Этот сценарий PowerShell должен запускаться локально на ПК или сервере, подключенном к Интернету.</span><span class="sxs-lookup"><span data-stu-id="f40c8-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f40c8-296">При запуске этого сценария могут выдаваться предупреждения и другие информационные сообщения PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f40c8-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="f40c8-297">Обращать внимание следует только на сообщения об ошибках, выделенные красным цветом.</span><span class="sxs-lookup"><span data-stu-id="f40c8-297">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

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
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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


#### <a name="network-config-file"></a><span data-ttu-id="f40c8-298">Файл конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="f40c8-298">Network Config File</span></span>
<span data-ttu-id="f40c8-299">Сохраните этот файл xml с новое местоположение и добавьте ссылку toothis hello файл toohello $NetworkConfigFile переменной в представленном выше сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="f40c8-299">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="f40c8-300">Сценарии примера приложения</span><span class="sxs-lookup"><span data-stu-id="f40c8-300">Sample Application Scripts</span></span>
<span data-ttu-id="f40c8-301">При желании tooinstall образец приложения для этого и других примерах DMZ, оно предоставлено в hello по ссылке: [образец приложения скрипта][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="f40c8-301">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Входящая сеть периметра с группой безопасности сети"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Значок NAT назначения"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Правило брандмауэра"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Активация правила брандмауэра"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
