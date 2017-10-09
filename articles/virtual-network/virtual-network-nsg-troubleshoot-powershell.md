---
title: "aaaTroubleshoot Сетевые группы безопасности - PowerShell | Документы Microsoft"
description: "Узнайте, как tootroubleshoot сетевых групп безопасности в развертывании диспетчера ресурсов Azure hello модели с помощью Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="516a5-103">Устранение неполадок, связанных с группами безопасности сети, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="516a5-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="516a5-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="516a5-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="516a5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="516a5-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="516a5-106">Если вы настроили группы безопасности сети (Nsg) на виртуальной машине (VM) и возникают проблемы с подключением виртуальных Машин, в этой статье Обзор возможностей диагностики для Nsg toohelp дополнительную диагностику.</span><span class="sxs-lookup"><span data-stu-id="516a5-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="516a5-107">Группы Nsg позволяют toocontrol hello типов трафика этого потока и из нее виртуальные машины (VM).</span><span class="sxs-lookup"><span data-stu-id="516a5-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="516a5-108">Nsg может быть применен toosubnets в виртуальной сети Azure (VNet) и сетевых интерфейсов (NIC).</span><span class="sxs-lookup"><span data-stu-id="516a5-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="516a5-109">Hello действующие правила, применяемые tooa сетевого Адаптера являются агрегата hello правил, которые существуют в hello Nsg применяется tooa сетевого Адаптера и hello подсети, в которой он подключен.</span><span class="sxs-lookup"><span data-stu-id="516a5-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="516a5-110">Правила в этих NSG иногда конфликтуют друг с другом и влияют на возможность сетевого подключения к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="516a5-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="516a5-111">Можно просмотреть все правила hello эффективной защиты от Nsg, применения сетевых адаптеров Виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="516a5-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="516a5-112">В этой статье показано, как с помощью этих правил в ВМ неполадок tootroubleshoot hello модели развертывания диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="516a5-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="516a5-113">Если вы не знакомы с основными понятиями виртуальной сети и NSG, прочтите hello [виртуальная сеть](virtual-networks-overview.md) и [сетевых групп безопасности](virtual-networks-nsg.md) Обзор статей.</span><span class="sxs-lookup"><span data-stu-id="516a5-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="516a5-114">С помощью поток трафика виртуальных Машин tootroubleshoot действующие правила безопасности</span><span class="sxs-lookup"><span data-stu-id="516a5-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="516a5-115">Hello сценарий, который следует за примером может служить распространенная проблема подключения:</span><span class="sxs-lookup"><span data-stu-id="516a5-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="516a5-116">Виртуальная машина с именем *VM1* принадлежит к подсети *Subnet1* в виртуальной сети *WestUS-VNet1*.</span><span class="sxs-lookup"><span data-stu-id="516a5-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="516a5-117">Попытка tooconnect toohello виртуальную Машину с помощью протокола удаленного рабочего СТОЛА через TCP-порт 3389 завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="516a5-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="516a5-118">Nsg применяются на обеих hello Сетевых *VM1 NIC1* и hello подсети *подсети1*.</span><span class="sxs-lookup"><span data-stu-id="516a5-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="516a5-119">Трафик tooTCP порт 3389 допускается в hello NSG, связанный с сетевым интерфейсом hello *VM1 NIC1*, однако в tooVM1 порт 3389 сбой проверить связь с TCP.</span><span class="sxs-lookup"><span data-stu-id="516a5-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="516a5-120">Здравствуйте, хотя в этом примере используется TCP-порт 3389, следующие действия можно используется toodetermine сбоев входящие и исходящие подключения через любой порт.</span><span class="sxs-lookup"><span data-stu-id="516a5-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="516a5-121">Подробные инструкции по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="516a5-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="516a5-122">Выполните следующие шаги tootroubleshoot Nsg для виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="516a5-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="516a5-123">Запуск сеанса и имени входа tooAzure Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="516a5-123">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="516a5-124">Если вы не знакомы с использованием Azure PowerShell, прочтите hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.</span><span class="sxs-lookup"><span data-stu-id="516a5-124">If you're not familiar with using Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="516a5-125">Введите следующую команду, tooreturn все правила NSG применяется tooa сетевого Адаптера с именем hello *VM1 NIC1* в группе ресурсов hello *RG1*:</span><span class="sxs-lookup"><span data-stu-id="516a5-125">Enter hello following command tooreturn all NSG rules applied tooa NIC named *VM1-NIC1* in hello resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="516a5-126">Если вы не знаете имя hello сетевой карты, введите hello, следующая команда tooretrieve hello имена всех сетевых адаптеров в группе ресурсов:</span><span class="sxs-lookup"><span data-stu-id="516a5-126">If you don't know hello name of a NIC, enter hello following command tooretrieve hello names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="516a5-127">Hello ниже приведен образец hello действующие правила данные, возвращаемые для hello *VM1 NIC1* сетевого Адаптера:</span><span class="sxs-lookup"><span data-stu-id="516a5-127">hello following text is a sample of hello effective rules output returned for hello *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="516a5-128">Обратите внимание следующую информацию в выходных данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="516a5-128">Note hello following information in hello output:</span></span>
   
   * <span data-ttu-id="516a5-129">Существует два раздела **NetworkSecurityGroup**: один для подсети (*Subnet1*), а другой для сетевого интерфейса (*VM1-NIC1*).</span><span class="sxs-lookup"><span data-stu-id="516a5-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="516a5-130">В этом примере NSG был применен tooeach.</span><span class="sxs-lookup"><span data-stu-id="516a5-130">In this example, an NSG has been applied tooeach.</span></span>
   * <span data-ttu-id="516a5-131">**Ассоциация** показывает hello ресурсов (подсети или сетевого Адаптера) заданного NSG связана с.</span><span class="sxs-lookup"><span data-stu-id="516a5-131">**Association** shows hello resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="516a5-132">Если hello NSG ресурс перемещен часовым непосредственно перед выполнением этой команды, может потребоваться toowait через несколько секунд для hello tooreflect изменение в выходных данных команды hello.</span><span class="sxs-lookup"><span data-stu-id="516a5-132">If hello NSG resource is moved/disassociated immediately before running this command, you may need toowait a few seconds for hello change tooreflect in hello command output.</span></span> 
   * <span data-ttu-id="516a5-133">имена правил, которые начинаются с Привет *defaultSecurityRules*: создается при NSG, несколько правил безопасности по умолчанию создаются внутри него.</span><span class="sxs-lookup"><span data-stu-id="516a5-133">hello rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="516a5-134">Правила по умолчанию нельзя удалить, но они могут быть переопределены правилами с более высоким приоритетом.</span><span class="sxs-lookup"><span data-stu-id="516a5-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="516a5-135">Чтение hello [NSG Обзор](virtual-networks-nsg.md#default-rules) toolearn статьи о NSG по умолчанию правила безопасности.</span><span class="sxs-lookup"><span data-stu-id="516a5-135">Read hello [NSG overview](virtual-networks-nsg.md#default-rules) article toolearn more about NSG default security rules.</span></span>
   * <span data-ttu-id="516a5-136">**ExpandedAddressPrefix** расширяет hello префиксы адресов для тегов по умолчанию NSG.</span><span class="sxs-lookup"><span data-stu-id="516a5-136">**ExpandedAddressPrefix** expands hello address prefixes for NSG default tags.</span></span> <span data-ttu-id="516a5-137">Каждый тег обозначает несколько префиксов адресов.</span><span class="sxs-lookup"><span data-stu-id="516a5-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="516a5-138">Расширения hello тегов можно использовать при устранении неполадок подключения к виртуальной Машине из конкретного адреса префиксы.</span><span class="sxs-lookup"><span data-stu-id="516a5-138">Expansion of hello tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="516a5-139">Например, тег VIRTUAL_NETWORK с пиринг виртуальной сети, расширяется tooshow одноранговыми префиксы виртуальной сети в предыдущие hello выходные данные.</span><span class="sxs-lookup"><span data-stu-id="516a5-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands tooshow peered VNet prefixes in hello previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="516a5-140">Здравствуйте команды только показаны действующие правила, если NSG связана с подсетью, сетевой Адаптер или оба.</span><span class="sxs-lookup"><span data-stu-id="516a5-140">hello command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="516a5-141">Виртуальная машина может иметь несколько сетевых интерфейсов, для которых применяются разные NSG.</span><span class="sxs-lookup"><span data-stu-id="516a5-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="516a5-142">При устранении неполадок, выполните команду hello для каждого сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="516a5-142">When troubleshooting, run hello command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="516a5-143">Фильтрация по большего количества правила NSG tooease введите следующие команды tootroubleshoot дальнейшей hello:</span><span class="sxs-lookup"><span data-stu-id="516a5-143">tooease filtering over larger number of NSG rules, enter hello following commands tootroubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="516a5-144">Фильтр для трафика RDP (TCP-порт 3389), применены toohello представление сетки, как показано в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="516a5-144">A filter for RDP traffic (TCP port 3389), is applied toohello grid view, as shown in hello following picture:</span></span>
   
    ![Список правил](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="516a5-146">Как видно в представлении сетки hello, существуют оба разрешающих и запрещающих правил для протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="516a5-146">As you can see in hello grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="516a5-147">Hello вывода из шага 2 показывает, что hello *DenyRDP* правило находится в подсети toohello NSG применяется hello.</span><span class="sxs-lookup"><span data-stu-id="516a5-147">hello output from step 2 shows that hello *DenyRDP* rule is in hello NSG applied toohello subnet.</span></span> <span data-ttu-id="516a5-148">Для входящих правил сначала обрабатываются Nsg применяется toohello подсети.</span><span class="sxs-lookup"><span data-stu-id="516a5-148">For inbound rules, NSGs applied toohello subnet are processed first.</span></span> <span data-ttu-id="516a5-149">Если соответствие найдено, hello NSG применяется toohello сетевого интерфейса не обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="516a5-149">If a match is found, hello NSG applied toohello network interface is not processed.</span></span> <span data-ttu-id="516a5-150">В этом случае hello *DenyRDP* правило из подсети hello блокирует toohello протокола удаленного рабочего СТОЛА виртуальной Машины (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="516a5-150">In this case, hello *DenyRDP* rule from hello subnet blocks RDP toohello VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="516a5-151">Виртуальная машина может иметь несколько сетевых адаптеров, подключенных tooit.</span><span class="sxs-lookup"><span data-stu-id="516a5-151">A VM may have multiple NICs attached tooit.</span></span> <span data-ttu-id="516a5-152">Каждый может быть подключенным tooa другой подсети.</span><span class="sxs-lookup"><span data-stu-id="516a5-152">Each may be connected tooa different subnet.</span></span> <span data-ttu-id="516a5-153">Поскольку команды hello в предыдущих шагах hello выполняются сетевой Адаптер, важно tooensure, указываемое hello возникают hello к сбою подключения к сетевой Адаптер.</span><span class="sxs-lookup"><span data-stu-id="516a5-153">Since hello commands in hello previous steps are run against a NIC, it's important tooensure that you specify hello NIC you're having hello connectivity failure to.</span></span> <span data-ttu-id="516a5-154">Если вы не знаете, можно всегда выполнить hello команды для каждого сетевого Адаптера, подключенного toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="516a5-154">If you're not sure, you can always run hello commands against each NIC attached toohello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="516a5-155">tooRDP в VM1 изменение hello *запретить RDP (3389)* правила слишком*Разрешить RDP(3389)* в hello **подсети1 NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="516a5-155">tooRDP into VM1, change hello *Deny RDP (3389)* rule too*Allow RDP(3389)* in hello **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="516a5-156">Убедитесь, что TCP-порт 3389 открыт путем открытия RDP соединение toohello ВМ или с помощью средства PsPing hello.</span><span class="sxs-lookup"><span data-stu-id="516a5-156">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="516a5-157">Дополнительные сведения о PsPing при чтении hello [PsPing загрузки страницы](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="516a5-157">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="516a5-158">Можно или удалить правила из NSG с помощью hello сведения в выходных данных hello hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="516a5-158">You can or remove rules from an NSG by using hello information in hello output from hello following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="516a5-159">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="516a5-159">Considerations</span></span>
<span data-ttu-id="516a5-160">Примите во внимание следующие точки, при устранении неполадок подключения hello.</span><span class="sxs-lookup"><span data-stu-id="516a5-160">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="516a5-161">Правила NSG по умолчанию будет блокировать входящий доступ из hello Интернета и только разрешения виртуальной сети для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="516a5-161">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="516a5-162">Правила должны быть явно добавлены tooallow входящий доступ из Интернета, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="516a5-162">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="516a5-163">Если нет правил безопасности NSG вызывает toofail подключения к сети Виртуальной машины, hello возможно, из-за:</span><span class="sxs-lookup"><span data-stu-id="516a5-163">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="516a5-164">Программный брандмауэр в операционной системе виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="516a5-164">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="516a5-165">Маршруты, настроенные для виртуальных устройств или локального трафика.</span><span class="sxs-lookup"><span data-stu-id="516a5-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="516a5-166">Интернет-трафик может быть перенаправленный tooon организациями через Принудительное туннелирование.</span><span class="sxs-lookup"><span data-stu-id="516a5-166">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="516a5-167">Этот параметр, в зависимости от того, как hello в локальной сети оборудования обрабатывает трафик RDP/SSH-подключения из Интернета hello tooyour виртуальной Машины будут недоступны.</span><span class="sxs-lookup"><span data-stu-id="516a5-167">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="516a5-168">Чтение hello [Устранение неполадок маршруты](virtual-network-routes-troubleshoot-powershell.md) статьи toolearn toodiagnose маршрут проблемы, которые могут не задерживают hello поток трафика в и из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="516a5-168">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="516a5-169">Если одноранговыми виртуальных сетей, по умолчанию, hello VIRTUAL_NETWORK тег автоматически расширяет tooinclude префиксы для одноранговыми виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="516a5-169">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="516a5-170">Можно просмотреть эти префиксы в hello **ExpandedAddressPrefix** список, tootroubleshoot любые проблемы связанные tooVNet пиринг подключения.</span><span class="sxs-lookup"><span data-stu-id="516a5-170">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="516a5-171">Правила безопасности отображаются, только если имеется NSG, связанный с виртуальной Машины hello сетевой Адаптер и или подсети.</span><span class="sxs-lookup"><span data-stu-id="516a5-171">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="516a5-172">Если Nsg, не связанные с hello сетевого Адаптера или подсети и имеется открытый IP-адрес, назначенный tooyour виртуальной Машины, все порты будут открыты для входящего и исходящего доступа.</span><span class="sxs-lookup"><span data-stu-id="516a5-172">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="516a5-173">Если виртуальная машина hello общедоступный IP-адрес, применение toohello Nsg сетевой Адаптер или подсети настоятельно рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="516a5-173">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>  

