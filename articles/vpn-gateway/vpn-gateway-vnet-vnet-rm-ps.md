---
title: "Подключение виртуальной сети Azure tooanother виртуальной сети: PowerShell | Документы Microsoft"
description: "Эта статья описывает этапы настройки подключения между виртуальными сетями с помощью диспетчера ресурсов Azure и PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="4fff8-103">Настройка подключения VPN-шлюза между виртуальными сетями с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fff8-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="4fff8-104">В этой статье показано, как toocreate шлюза VPN-подключение между виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="4fff8-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="4fff8-105">Hello виртуальные сети могут находиться в Здравствуйте, или же в разных регионах, и из hello таким же или разных подписках.</span><span class="sxs-lookup"><span data-stu-id="4fff8-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="4fff8-106">При подключении виртуальных сетей из разных подписок, подписки hello не обязательно toobe, связанный с hello того же клиента Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4fff8-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="4fff8-107">в этой статье инструкциям Hello применяются toohello модели развертывания диспетчера ресурсов и с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fff8-107">hello steps in this article apply toohello Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="4fff8-108">Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.</span><span class="sxs-lookup"><span data-stu-id="4fff8-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fff8-109">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4fff8-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="4fff8-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fff8-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="4fff8-111">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="4fff8-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="4fff8-112">Портал Azure (классический)</span><span class="sxs-lookup"><span data-stu-id="4fff8-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="4fff8-113">Подключение с использованием разных моделей развертывания — портал Azure</span><span class="sxs-lookup"><span data-stu-id="4fff8-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="4fff8-114">Подключение с использованием разных моделей развертывания — PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fff8-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="4fff8-115">Подключение виртуальной сети tooanother виртуальной сети (VNet-VNet) — примерно tooconnecting локального сайта виртуальной сети tooan расположения.</span><span class="sxs-lookup"><span data-stu-id="4fff8-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="4fff8-116">Оба типа подключения используйте tooprovide шлюза VPN защищенный туннель, с помощью IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="4fff8-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="4fff8-117">Если ваш виртуальных сетей в hello совпадают, вы можете tooconsider подключаются с помощью Пиринг виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4fff8-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="4fff8-118">При пиринговой связи между виртуальными сетями VPN-шлюз не используется.</span><span class="sxs-lookup"><span data-stu-id="4fff8-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="4fff8-119">Дополнительную информацию см. в статье [Пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fff8-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="4fff8-120">Подключение типа "виртуальная сеть — виртуальная сеть" можно комбинировать с многосайтовыми конфигурациями.</span><span class="sxs-lookup"><span data-stu-id="4fff8-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="4fff8-121">Это дает возможность установления сетевых топологий, которые объединяют подключения между организациями с подключением между виртуальными сетями, как показано в hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="4fff8-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Сведения о подключениях](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="4fff8-123">Что может дать связь между виртуальными сетями</span><span class="sxs-lookup"><span data-stu-id="4fff8-123">Why connect virtual networks?</span></span>

<span data-ttu-id="4fff8-124">Вы можете tooconnect виртуальных сетей для hello следующих причин:</span><span class="sxs-lookup"><span data-stu-id="4fff8-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="4fff8-125">**Межрегиональная географическая избыточность и географическое присутствие**</span><span class="sxs-lookup"><span data-stu-id="4fff8-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="4fff8-126">Вы можете настроить собственную георепликацию или синхронизацию с безопасной связью без прохождения трафика через конечные точки с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="4fff8-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="4fff8-127">С помощью Azure Load Balancer и диспетчера трафика можно настроить высокодоступную рабочую нагрузку с геоизбыточностью в нескольких регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="4fff8-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="4fff8-128">Важный пример — tooset копии SQL Always On с группами доступности, распределение по нескольким регионам Azure.</span><span class="sxs-lookup"><span data-stu-id="4fff8-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="4fff8-129">**Региональные многоуровневые приложения с изоляцией или административной границей**</span><span class="sxs-lookup"><span data-stu-id="4fff8-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="4fff8-130">В пределах hello же регионе, можно настроить многоуровневые приложения с несколькими виртуальными сетями, которые соединены друг с другом, из-за tooisolation или требований администрирования.</span><span class="sxs-lookup"><span data-stu-id="4fff8-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="4fff8-131">Дополнительные сведения о подключениях к виртуальной сети для виртуальной сети см. в разделе hello [часто задаваемые вопросы о виртуальной сети для виртуальной сети](#faq) конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4fff8-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="4fff8-132">Каким инструкциям следовать?</span><span class="sxs-lookup"><span data-stu-id="4fff8-132">Which set of steps should I use?</span></span>

<span data-ttu-id="4fff8-133">В этой статье приведены два разных набора действий.</span><span class="sxs-lookup"><span data-stu-id="4fff8-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="4fff8-134">Один набор шагов для [Здравствуйте, виртуальных сетей, которые находятся в одной подписке](#samesub), а другой — [виртуальных сетей, которые находятся в разных подписках](#difsub).</span><span class="sxs-lookup"><span data-stu-id="4fff8-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="4fff8-135">Hello ключевое различие между наборами hello — можно создать и настроить все виртуальные ресурсы сети и шлюза hello одного сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fff8-135">hello key difference between hello sets is whether you can create and configure all virtual network and gateway resources within hello same PowerShell session.</span></span>

<span data-ttu-id="4fff8-136">Hello действия, описанные в этой статье использовать переменные, объявленные в начале каждого раздела hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-136">hello steps in this article use variables that are declared at hello beginning of each section.</span></span> <span data-ttu-id="4fff8-137">Если вы уже работаете с существующие виртуальные сети, измените параметры hello переменные tooreflect hello в собственной среде.</span><span class="sxs-lookup"><span data-stu-id="4fff8-137">If you already are working with existing VNets, modify hello variables tooreflect hello settings in your own environment.</span></span> <span data-ttu-id="4fff8-138">Сведения о разрешении имен виртуальных машин см. в [этой статье](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="4fff8-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="4fff8-139"><a name="samesub"></a>Как tooconnect виртуальных сетей, находящихся в hello одной подписке</span><span class="sxs-lookup"><span data-stu-id="4fff8-139"><a name="samesub"></a>How tooconnect VNets that are in hello same subscription</span></span>

![Схема подключения между виртуальными сетями](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="4fff8-141">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="4fff8-141">Before you begin</span></span>

<span data-ttu-id="4fff8-142">Прежде чем начать, необходимо tooinstall hello последняя версия командлетов Azure PowerShell диспетчера ресурсов hello, по крайней мере версии 4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="4fff8-142">Before beginning, you need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="4fff8-143">Дополнительные сведения об установке hello командлеты PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4fff8-143">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="4fff8-144"><a name="Step1"></a>Шаг 1. Планирование диапазонов IP-адресов</span><span class="sxs-lookup"><span data-stu-id="4fff8-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="4fff8-145">В hello, выполнив действия мы создадим два виртуальных сетей вместе с их соответствующими шлюза подсетях и конфигурациях.</span><span class="sxs-lookup"><span data-stu-id="4fff8-145">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="4fff8-146">Затем создадим VPN-подключение между hello двух виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="4fff8-146">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="4fff8-147">Это важные tooplan hello IP-адресов для настройки сети.</span><span class="sxs-lookup"><span data-stu-id="4fff8-147">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="4fff8-148">Имейте в виду, необходимо убедиться в том, что ни один из диапазонов виртуальных сетей или диапазонов локальных сетей никак не перекрываются.</span><span class="sxs-lookup"><span data-stu-id="4fff8-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="4fff8-149">В этих примерах мы не включаем DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="4fff8-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="4fff8-150">Сведения о разрешении имен виртуальных машин см. в [этой статье](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="4fff8-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="4fff8-151">Мы используем следующие значения в примерах hello hello:</span><span class="sxs-lookup"><span data-stu-id="4fff8-151">We use hello following values in hello examples:</span></span>

<span data-ttu-id="4fff8-152">**Значения для TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="4fff8-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="4fff8-153">Имя виртуальной сети: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4fff8-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="4fff8-154">Группа ресурсов: TestRG1</span><span class="sxs-lookup"><span data-stu-id="4fff8-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="4fff8-155">Расположение: восточная часть США</span><span class="sxs-lookup"><span data-stu-id="4fff8-155">Location: East US</span></span>
* <span data-ttu-id="4fff8-156">TestVNet1: 10.11.0.0/16 и 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4fff8-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="4fff8-157">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fff8-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="4fff8-158">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fff8-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="4fff8-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="4fff8-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="4fff8-160">Имя шлюза: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="4fff8-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="4fff8-161">Общедоступный IP-адрес: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="4fff8-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="4fff8-162">Тип VPN: RouteBased</span><span class="sxs-lookup"><span data-stu-id="4fff8-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="4fff8-163">Подключение (1–4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="4fff8-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="4fff8-164">Подключение (1–5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="4fff8-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="4fff8-165">Тип подключения: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="4fff8-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="4fff8-166">**Значения для TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="4fff8-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="4fff8-167">Имя виртуальной сети: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="4fff8-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="4fff8-168">TestVNet2: 10.41.0.0/16 и 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4fff8-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="4fff8-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fff8-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="4fff8-170">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fff8-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="4fff8-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="4fff8-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="4fff8-172">Группа ресурсов: TestRG4</span><span class="sxs-lookup"><span data-stu-id="4fff8-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="4fff8-173">Расположение: Запад США</span><span class="sxs-lookup"><span data-stu-id="4fff8-173">Location: West US</span></span>
* <span data-ttu-id="4fff8-174">Имя шлюза: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="4fff8-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="4fff8-175">Общедоступный IP-адрес: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="4fff8-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="4fff8-176">Тип VPN: RouteBased</span><span class="sxs-lookup"><span data-stu-id="4fff8-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="4fff8-177">Подключение: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="4fff8-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="4fff8-178">Тип подключения: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="4fff8-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="4fff8-179"><a name="Step2"></a>Шаг 2. Создание и настройка TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4fff8-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="4fff8-180">Объявите переменные.</span><span class="sxs-lookup"><span data-stu-id="4fff8-180">Declare your variables.</span></span> <span data-ttu-id="4fff8-181">В этом примере hello переменных объявляются с помощью hello значения для этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="4fff8-181">This example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="4fff8-182">В большинстве случаев следует заменить значения hello свои собственные.</span><span class="sxs-lookup"><span data-stu-id="4fff8-182">In most cases, you should replace hello values with your own.</span></span> <span data-ttu-id="4fff8-183">Тем не менее эти переменные можно использовать при выполнении через toobecome действия hello знакомы с этим типом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4fff8-183">However, you can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="4fff8-184">Изменение переменных hello, при необходимости, а затем скопируйте и вставьте их в консоль PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fff8-184">Modify hello variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. <span data-ttu-id="4fff8-185">Подключите tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="4fff8-185">Connect tooyour account.</span></span> <span data-ttu-id="4fff8-186">Используйте следующий пример toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-186">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="4fff8-187">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-187">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="4fff8-188">Укажите требуемый toouse подписки hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-188">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="4fff8-189">Создайте новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4fff8-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="4fff8-190">Создание конфигурации подсети для TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-190">Create hello subnet configurations for TestVNet1.</span></span> <span data-ttu-id="4fff8-191">В этом примере создается виртуальная сеть с именем TestVNet1 и три подсети: GatewaySubnet, FrontEnd и Backend.</span><span class="sxs-lookup"><span data-stu-id="4fff8-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="4fff8-192">При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="4fff8-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="4fff8-193">Если вы используете другое имя, создание шлюза завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="4fff8-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="4fff8-194">Hello следующий пример использует переменные hello, было установлено ранее.</span><span class="sxs-lookup"><span data-stu-id="4fff8-194">hello following example uses hello variables that you set earlier.</span></span> <span data-ttu-id="4fff8-195">В этом примере hello подсеть шлюза используется /27.</span><span class="sxs-lookup"><span data-stu-id="4fff8-195">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="4fff8-196">Хотя возможных toocreate как /29 подсеть шлюза, рекомендуется создать подсеть большего размера, включающий несколько адресов, выбрав по крайней мере /28 или /27.</span><span class="sxs-lookup"><span data-stu-id="4fff8-196">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="4fff8-197">Это позволит достаточно адреса tooaccommodate возможные дополнительные настройки, вы можете в hello будущих.</span><span class="sxs-lookup"><span data-stu-id="4fff8-197">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="4fff8-198">Создайте TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fff8-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="4fff8-199">Запрос открытый IP-адрес toobe toohello выделенный шлюз, создаваемых для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4fff8-199">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="4fff8-200">Обратите внимание, что hello AllocationMethod является динамической.</span><span class="sxs-lookup"><span data-stu-id="4fff8-200">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="4fff8-201">Нельзя указать hello IP-адреса, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="4fff8-201">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="4fff8-202">Он служит шлюзом динамически выделяемый tooyour.</span><span class="sxs-lookup"><span data-stu-id="4fff8-202">It's dynamically allocated tooyour gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="4fff8-203">Создайте конфигурацию шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-203">Create hello gateway configuration.</span></span> <span data-ttu-id="4fff8-204">Конфигурация шлюза Hello определяет подсеть hello и hello открытый IP адрес toouse.</span><span class="sxs-lookup"><span data-stu-id="4fff8-204">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="4fff8-205">Используйте toocreate пример hello конфигурацию шлюза.</span><span class="sxs-lookup"><span data-stu-id="4fff8-205">Use hello example toocreate your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="4fff8-206">Создайте шлюз hello для TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fff8-206">Create hello gateway for TestVNet1.</span></span> <span data-ttu-id="4fff8-207">На этом шаге создается hello шлюз виртуальной сети для вашего TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fff8-207">In this step, you create hello virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="4fff8-208">Для подключений типа VNet-to-VNet необходимо использовать тип VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="4fff8-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="4fff8-209">Создание шлюза часто занимает 45 минут или более, в зависимости от выбранного шлюза hello SKU.</span><span class="sxs-lookup"><span data-stu-id="4fff8-209">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="4fff8-210">Шаг 3. Создание и настройка TestVNet4</span><span class="sxs-lookup"><span data-stu-id="4fff8-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="4fff8-211">После настройки TestVNet1 создайте TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4fff8-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="4fff8-212">Выполните действия hello ниже замена значений hello собственными при необходимости.</span><span class="sxs-lookup"><span data-stu-id="4fff8-212">Follow hello steps below, replacing hello values with your own when needed.</span></span> <span data-ttu-id="4fff8-213">Этот шаг можно выполнить в hello же сеанс PowerShell, так как он находится в hello же подписки.</span><span class="sxs-lookup"><span data-stu-id="4fff8-213">This step can be done within hello same PowerShell session because it is in hello same subscription.</span></span>

1. <span data-ttu-id="4fff8-214">Объявите переменные.</span><span class="sxs-lookup"><span data-stu-id="4fff8-214">Declare your variables.</span></span> <span data-ttu-id="4fff8-215">Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4fff8-215">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. <span data-ttu-id="4fff8-216">Создайте новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4fff8-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="4fff8-217">Создание конфигурации подсети для TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-217">Create hello subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="4fff8-218">Создайте TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4fff8-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="4fff8-219">Запросите общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4fff8-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="4fff8-220">Создайте конфигурацию шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-220">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="4fff8-221">Создайте шлюз TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-221">Create hello TestVNet4 gateway.</span></span> <span data-ttu-id="4fff8-222">Создание шлюза часто занимает 45 минут или более, в зависимости от выбранного шлюза hello SKU.</span><span class="sxs-lookup"><span data-stu-id="4fff8-222">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a><span data-ttu-id="4fff8-223">Шаг 4 — Создание подключений hello</span><span class="sxs-lookup"><span data-stu-id="4fff8-223">Step 4 - Create hello connections</span></span>

1. <span data-ttu-id="4fff8-224">Получите оба шлюза для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="4fff8-224">Get both virtual network gateways.</span></span> <span data-ttu-id="4fff8-225">При выполнении обоих шлюзов hello hello одной подписке, как в примере hello, можно выполнить на этом шаге hello одного сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fff8-225">If both of hello gateways are in hello same subscription, as they are in hello example, you can complete this step in hello same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="4fff8-226">Создание подключения tooTestVNet4 TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-226">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="4fff8-227">На этом этапе можно создать подключение hello TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4fff8-227">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="4fff8-228">Вы увидите общий ключ, на который ссылается примеры hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-228">You'll see a shared key referenced in hello examples.</span></span> <span data-ttu-id="4fff8-229">Можно использовать собственные значения для hello общего ключа.</span><span class="sxs-lookup"><span data-stu-id="4fff8-229">You can use your own values for hello shared key.</span></span> <span data-ttu-id="4fff8-230">Важно, что это общий ключ, hello Hello оба соединения должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="4fff8-230">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="4fff8-231">Создание соединения может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4fff8-231">Creating a connection can take a short while toocomplete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="4fff8-232">Создание подключения tooTestVNet1 TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-232">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="4fff8-233">Этот шаг является аналогичные toohello показано выше, за исключением того, вы создаете подключение hello из TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fff8-233">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="4fff8-234">Убедитесь, что hello общие ключи совпадают.</span><span class="sxs-lookup"><span data-stu-id="4fff8-234">Make sure hello shared keys match.</span></span> <span data-ttu-id="4fff8-235">будет установлено подключение Hello через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4fff8-235">hello connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="4fff8-236">Проверьте подключение.</span><span class="sxs-lookup"><span data-stu-id="4fff8-236">Verify your connection.</span></span> <span data-ttu-id="4fff8-237">В разделе hello [как tooverify подключения](#verify).</span><span class="sxs-lookup"><span data-stu-id="4fff8-237">See hello section [How tooverify your connection](#verify).</span></span>

## <span data-ttu-id="4fff8-238"><a name="difsub"></a>Как tooconnect виртуальных сетей, находящихся в разных подписках</span><span class="sxs-lookup"><span data-stu-id="4fff8-238"><a name="difsub"></a>How tooconnect VNets that are in different subscriptions</span></span>

![Схема подключения между виртуальными сетями](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="4fff8-240">В этом сценарии мы создадим подключение между TestVNet1 и TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4fff8-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="4fff8-241">TestVNet1 и TestVNet5 находятся в разных подписках.</span><span class="sxs-lookup"><span data-stu-id="4fff8-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="4fff8-242">Hello подписки не обязательно toobe, связанный с hello того же клиента Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4fff8-242">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="4fff8-243">Hello эти действия и предыдущий набор hello отличается некоторые шаги настройки hello необходимость toobe выполняется в отдельном сеансе PowerShell, в контексте hello hello второй подписки.</span><span class="sxs-lookup"><span data-stu-id="4fff8-243">hello difference between these steps and hello previous set is that some of hello configuration steps need toobe performed in a separate PowerShell session in hello context of hello second subscription.</span></span> <span data-ttu-id="4fff8-244">Особенно при hello двух подписок принадлежат toodifferent организаций.</span><span class="sxs-lookup"><span data-stu-id="4fff8-244">Especially when hello two subscriptions belong toodifferent organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="4fff8-245">Шаг 5. Создание и настройка TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4fff8-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="4fff8-246">Необходимо выполнить [шаг 1](#Step1) и [шаг 2](#Step2) из hello предыдущей статьи toocreate и настроить TestVNet1 и hello VPN-шлюза для TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fff8-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from hello previous section toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="4fff8-247">Для этой конфигурации не требуется toocreate TestVNet4 hello в предыдущем разделе, несмотря на то, что при ее создании, оно не будет конфликтовать с следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4fff8-247">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="4fff8-248">После выполнения шага 1 и 2 шага, выполните шаг 6 toocreate TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4fff8-248">Once you complete Step 1 and Step 2, continue with Step 6 toocreate TestVNet5.</span></span> 

### <a name="step-6---verify-hello-ip-address-ranges"></a><span data-ttu-id="4fff8-249">Шаг 6 - проверка hello диапазоны IP-адресов</span><span class="sxs-lookup"><span data-stu-id="4fff8-249">Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="4fff8-250">Это важные toomake в том, что пространство IP-адресов hello hello новой виртуальной сети, TestVNet5, не перекрываются с любым из диапазонов сети VNet или диапазоны шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="4fff8-250">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="4fff8-251">В этом примере hello виртуальных сетей может принадлежать toodifferent организаций.</span><span class="sxs-lookup"><span data-stu-id="4fff8-251">In this example, hello virtual networks may belong toodifferent organizations.</span></span> <span data-ttu-id="4fff8-252">Для этого упражнения можно использовать следующие значения для hello TestVNet5 hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-252">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="4fff8-253">**Значения для TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="4fff8-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="4fff8-254">Имя виртуальной сети: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="4fff8-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="4fff8-255">Группа ресурсов: TestRG5</span><span class="sxs-lookup"><span data-stu-id="4fff8-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="4fff8-256">Расположение: восточная часть Японии</span><span class="sxs-lookup"><span data-stu-id="4fff8-256">Location: Japan East</span></span>
* <span data-ttu-id="4fff8-257">TestVNet5: 10.51.0.0/16 и 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4fff8-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="4fff8-258">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fff8-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="4fff8-259">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fff8-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="4fff8-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="4fff8-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="4fff8-261">Имя шлюза: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="4fff8-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="4fff8-262">Общедоступный IP-адрес: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="4fff8-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="4fff8-263">Тип VPN: RouteBased</span><span class="sxs-lookup"><span data-stu-id="4fff8-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="4fff8-264">Подключение: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="4fff8-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="4fff8-265">Тип подключения: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="4fff8-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="4fff8-266">Шаг 7. Создание и настройка TestVNet5</span><span class="sxs-lookup"><span data-stu-id="4fff8-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="4fff8-267">Этот шаг необходимо выполнить в контексте hello hello новую подписку.</span><span class="sxs-lookup"><span data-stu-id="4fff8-267">This step must be done in hello context of hello new subscription.</span></span> <span data-ttu-id="4fff8-268">Эта часть может выполняться Здравствуйте, администратор в другой организации, которой принадлежит подписка hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-268">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span>

1. <span data-ttu-id="4fff8-269">Объявите переменные.</span><span class="sxs-lookup"><span data-stu-id="4fff8-269">Declare your variables.</span></span> <span data-ttu-id="4fff8-270">Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4fff8-270">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="4fff8-271">Подключите toosubscription 5.</span><span class="sxs-lookup"><span data-stu-id="4fff8-271">Connect toosubscription 5.</span></span> <span data-ttu-id="4fff8-272">Откройте консоль PowerShell и подключить tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="4fff8-272">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="4fff8-273">Используйте следующий пример toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-273">Use hello following sample toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="4fff8-274">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-274">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="4fff8-275">Укажите требуемый toouse подписки hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-275">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="4fff8-276">Создайте новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4fff8-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="4fff8-277">Создание конфигурации подсети для TestVNet5 hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-277">Create hello subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="4fff8-278">Создайте TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4fff8-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="4fff8-279">Запросите общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4fff8-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="4fff8-280">Создайте конфигурацию шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-280">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="4fff8-281">Создайте шлюз TestVNet5 hello.</span><span class="sxs-lookup"><span data-stu-id="4fff8-281">Create hello TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a><span data-ttu-id="4fff8-282">Шаг 8 — Создание подключений hello</span><span class="sxs-lookup"><span data-stu-id="4fff8-282">Step 8 - Create hello connections</span></span>

<span data-ttu-id="4fff8-283">В этом примере так как шлюзы hello находятся в разных подписках hello, мы разбить этот шаг двух сеансов PowerShell, помеченный как [подписки 1] и [подписки 5].</span><span class="sxs-lookup"><span data-stu-id="4fff8-283">In this example, because hello gateways are in hello different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="4fff8-284">**[Подписки 1]**  Шлюз виртуальной сети hello get для подписки 1.</span><span class="sxs-lookup"><span data-stu-id="4fff8-284">**[Subscription 1]** Get hello virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="4fff8-285">Вход и подключиться tooSubscription 1 перед запуском hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4fff8-285">Log in and connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="4fff8-286">Копировать выходные данные hello hello следующие элементы и отправлять эти администратора toohello 5 подписки по электронной почте или другим методом.</span><span class="sxs-lookup"><span data-stu-id="4fff8-286">Copy hello output of hello following elements and send these toohello administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="4fff8-287">Эти два элемента будет иметь примерно toohello значения следующий пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="4fff8-287">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="4fff8-288">**[Подписки 5]**  Шлюз виртуальной сети hello get для 5 подписки.</span><span class="sxs-lookup"><span data-stu-id="4fff8-288">**[Subscription 5]** Get hello virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="4fff8-289">Вход и подключиться tooSubscription 5 перед запуском hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4fff8-289">Log in and connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="4fff8-290">Копировать выходные данные hello hello следующие элементы и отправлять эти администратора toohello 1 подписки по электронной почте или другим методом.</span><span class="sxs-lookup"><span data-stu-id="4fff8-290">Copy hello output of hello following elements and send these toohello administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="4fff8-291">Эти два элемента будет иметь примерно toohello значения следующий пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="4fff8-291">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="4fff8-292">**[Подписки 1]**  Создать hello TestVNet1 tooTestVNet5 соединение.</span><span class="sxs-lookup"><span data-stu-id="4fff8-292">**[Subscription 1]** Create hello TestVNet1 tooTestVNet5 connection.</span></span> <span data-ttu-id="4fff8-293">На этом этапе можно создать подключение hello TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4fff8-293">In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="4fff8-294">Hello различие — $vnet5gw не удается получить напрямую, так как он находится в другой подписке.</span><span class="sxs-lookup"><span data-stu-id="4fff8-294">hello difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="4fff8-295">Вам потребуется toocreate объекта PowerShell со значениями hello, переданные от подписки 1 в hello описанные выше действия.</span><span class="sxs-lookup"><span data-stu-id="4fff8-295">You will need toocreate a new PowerShell object with hello values communicated from Subscription 1 in hello steps above.</span></span> <span data-ttu-id="4fff8-296">Используйте hello. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="4fff8-296">Use hello example below.</span></span> <span data-ttu-id="4fff8-297">Замените собственными значениями hello имя, идентификатор и общего ключа.</span><span class="sxs-lookup"><span data-stu-id="4fff8-297">Replace hello Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="4fff8-298">Важно, что это общий ключ, hello Hello оба соединения должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="4fff8-298">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="4fff8-299">Создание соединения может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4fff8-299">Creating a connection can take a short while toocomplete.</span></span>

  <span data-ttu-id="4fff8-300">Перед выполнением следующий пример hello подключите tooSubscription 1:</span><span class="sxs-lookup"><span data-stu-id="4fff8-300">Connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="4fff8-301">**[Подписки 5]**  Создать hello TestVNet5 tooTestVNet1 соединение.</span><span class="sxs-lookup"><span data-stu-id="4fff8-301">**[Subscription 5]** Create hello TestVNet5 tooTestVNet1 connection.</span></span> <span data-ttu-id="4fff8-302">Этот шаг является аналогичные toohello показано выше, за исключением того, вы создаете подключение hello из TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fff8-302">This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="4fff8-303">Hello же процесс создания объекта PowerShell, на основании hello значения, полученные из подписки 1 относится здесь также.</span><span class="sxs-lookup"><span data-stu-id="4fff8-303">hello same process of creating a PowerShell object based on hello values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="4fff8-304">На этом шаге убедитесь, что hello общие ключи совпадают.</span><span class="sxs-lookup"><span data-stu-id="4fff8-304">In this step, be sure that hello shared keys match.</span></span>

  <span data-ttu-id="4fff8-305">Перед выполнением следующий пример hello подключите tooSubscription 5:</span><span class="sxs-lookup"><span data-stu-id="4fff8-305">Connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="4fff8-306"><a name="verify"></a>Как tooverify соединение</span><span class="sxs-lookup"><span data-stu-id="4fff8-306"><a name="verify"></a>How tooverify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="4fff8-307"><a name="faq"></a>Часто задаваемые вопросы о подключениях типа "виртуальная сеть — виртуальная сеть"</span><span class="sxs-lookup"><span data-stu-id="4fff8-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4fff8-308">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4fff8-308">Next steps</span></span>

* <span data-ttu-id="4fff8-309">После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="4fff8-309">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="4fff8-310">В разделе hello [документация по виртуальным машинам](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="4fff8-310">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="4fff8-311">Сведения о BGP см. в разделе hello [Обзор BGP](vpn-gateway-bgp-overview.md) и [как tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4fff8-311">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
