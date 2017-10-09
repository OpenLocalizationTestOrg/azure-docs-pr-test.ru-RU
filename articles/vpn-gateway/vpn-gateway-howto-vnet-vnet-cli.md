---
title: "Подключение виртуальной сети tooanother виртуальной сети: Azure CLI | Документы Microsoft"
description: "В этой статье описаны этапы настройки подключения между виртуальными сетями с помощью Azure Resource Manager и Azure CLI."
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
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="a2143-103">Настройка подключения VPN-шлюза между виртуальными сетями с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a2143-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="a2143-104">В этой статье показано, как toocreate шлюза VPN-подключение между виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="a2143-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="a2143-105">Hello виртуальные сети могут находиться в Здравствуйте, или же в разных регионах, и из hello таким же или разных подписках.</span><span class="sxs-lookup"><span data-stu-id="a2143-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="a2143-106">При подключении виртуальных сетей из разных подписок, подписки hello не обязательно toobe, связанный с hello того же клиента Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a2143-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="a2143-107">в этой статье инструкциям Hello применить toohello модели развертывания диспетчера ресурсов и использовать Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a2143-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="a2143-108">Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.</span><span class="sxs-lookup"><span data-stu-id="a2143-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2143-109">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="a2143-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="a2143-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2143-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="a2143-111">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="a2143-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="a2143-112">Портал Azure (классический)</span><span class="sxs-lookup"><span data-stu-id="a2143-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="a2143-113">Подключение с использованием разных моделей развертывания — портал Azure</span><span class="sxs-lookup"><span data-stu-id="a2143-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="a2143-114">Подключение с использованием разных моделей развертывания — PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2143-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="a2143-115">Подключение виртуальной сети tooanother виртуальной сети (VNet-VNet) — примерно tooconnecting локального сайта виртуальной сети tooan расположения.</span><span class="sxs-lookup"><span data-stu-id="a2143-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="a2143-116">Оба типа подключения используйте tooprovide шлюза VPN защищенный туннель, с помощью IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="a2143-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="a2143-117">Если ваш виртуальных сетей в hello совпадают, вы можете tooconsider подключаются с помощью Пиринг виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a2143-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="a2143-118">При пиринговой связи между виртуальными сетями VPN-шлюз не используется.</span><span class="sxs-lookup"><span data-stu-id="a2143-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="a2143-119">Дополнительную информацию см. в статье [Пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2143-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="a2143-120">Подключение типа "виртуальная сеть — виртуальная сеть" можно комбинировать с многосайтовыми конфигурациями.</span><span class="sxs-lookup"><span data-stu-id="a2143-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="a2143-121">Это дает возможность установления сетевых топологий, которые объединяют подключения между организациями с подключением между виртуальными сетями, как показано в hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="a2143-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Сведения о подключениях](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="a2143-123"><a name="why"></a>Зачем нужна связь между виртуальными сетями?</span><span class="sxs-lookup"><span data-stu-id="a2143-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="a2143-124">Вы можете tooconnect виртуальных сетей для hello следующих причин:</span><span class="sxs-lookup"><span data-stu-id="a2143-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="a2143-125">**Межрегиональная географическая избыточность и географическое присутствие**</span><span class="sxs-lookup"><span data-stu-id="a2143-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="a2143-126">Вы можете настроить собственную георепликацию или синхронизацию с безопасной связью без прохождения трафика через конечные точки с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="a2143-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="a2143-127">С помощью Azure Load Balancer и диспетчера трафика можно настроить высокодоступную рабочую нагрузку с геоизбыточностью в нескольких регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="a2143-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="a2143-128">Важный пример — tooset копии SQL Always On с группами доступности, распределение по нескольким регионам Azure.</span><span class="sxs-lookup"><span data-stu-id="a2143-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="a2143-129">**Региональные многоуровневые приложения с изоляцией или административной границей**</span><span class="sxs-lookup"><span data-stu-id="a2143-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="a2143-130">В пределах hello же регионе, можно настроить многоуровневые приложения с несколькими виртуальными сетями, которые соединены друг с другом, из-за tooisolation или требований администрирования.</span><span class="sxs-lookup"><span data-stu-id="a2143-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="a2143-131">Дополнительные сведения о подключениях к виртуальной сети для виртуальной сети см. в разделе hello [часто задаваемые вопросы о виртуальной сети для виртуальной сети](#faq) конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a2143-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="a2143-132">Каким инструкциям следовать?</span><span class="sxs-lookup"><span data-stu-id="a2143-132">Which set of steps should I use?</span></span>

<span data-ttu-id="a2143-133">В этой статье приведены два разных набора действий.</span><span class="sxs-lookup"><span data-stu-id="a2143-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="a2143-134">Один набор шагов для [Здравствуйте, виртуальных сетей, которые находятся в одной подписке](#samesub), а другой — [виртуальных сетей, которые находятся в разных подписках](#difsub).</span><span class="sxs-lookup"><span data-stu-id="a2143-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="a2143-135"><a name="samesub"></a>Подключение виртуальных сетей, которые в hello одной подписке</span><span class="sxs-lookup"><span data-stu-id="a2143-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![Схема подключения между виртуальными сетями](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="a2143-137">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a2143-137">Before you begin</span></span>

<span data-ttu-id="a2143-138">Прежде чем начать, установите последнюю версию hello hello команды CLI (2.0 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="a2143-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="a2143-139">Сведения об установке hello командах CLI см. в разделе [установить CLI Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a2143-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="a2143-140"><a name="Plan"></a>Планирование диапазонов IP-адресов</span><span class="sxs-lookup"><span data-stu-id="a2143-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="a2143-141">В hello, выполнив действия мы создадим два виртуальных сетей вместе с их соответствующими шлюза подсетях и конфигурациях.</span><span class="sxs-lookup"><span data-stu-id="a2143-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="a2143-142">Затем создадим VPN-подключение между hello двух виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="a2143-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="a2143-143">Это важные tooplan hello IP-адресов для настройки сети.</span><span class="sxs-lookup"><span data-stu-id="a2143-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="a2143-144">Имейте в виду, необходимо убедиться в том, что ни один из диапазонов виртуальных сетей или диапазонов локальных сетей никак не перекрываются.</span><span class="sxs-lookup"><span data-stu-id="a2143-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="a2143-145">В этих примерах мы не включаем DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="a2143-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="a2143-146">Сведения о разрешении имен виртуальных машин см. в [этой статье](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="a2143-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="a2143-147">Мы используем следующие значения в примерах hello hello:</span><span class="sxs-lookup"><span data-stu-id="a2143-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="a2143-148">**Значения для TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="a2143-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="a2143-149">Имя виртуальной сети: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="a2143-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="a2143-150">Группа ресурсов: TestRG1</span><span class="sxs-lookup"><span data-stu-id="a2143-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="a2143-151">Расположение: восточная часть США</span><span class="sxs-lookup"><span data-stu-id="a2143-151">Location: East US</span></span>
* <span data-ttu-id="a2143-152">TestVNet1: 10.11.0.0/16 и 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a2143-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="a2143-153">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a2143-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="a2143-154">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a2143-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="a2143-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="a2143-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="a2143-156">Имя шлюза: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="a2143-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="a2143-157">Общедоступный IP-адрес: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="a2143-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="a2143-158">Тип VPN: RouteBased</span><span class="sxs-lookup"><span data-stu-id="a2143-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="a2143-159">Подключение (1–4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="a2143-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="a2143-160">Подключение (1–5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="a2143-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="a2143-161">Тип подключения: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="a2143-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="a2143-162">**Значения для TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="a2143-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="a2143-163">Имя виртуальной сети: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="a2143-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="a2143-164">TestVNet2: 10.41.0.0/16 и 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a2143-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="a2143-165">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a2143-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="a2143-166">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a2143-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="a2143-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="a2143-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="a2143-168">Группа ресурсов: TestRG4</span><span class="sxs-lookup"><span data-stu-id="a2143-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="a2143-169">Расположение: Запад США</span><span class="sxs-lookup"><span data-stu-id="a2143-169">Location: West US</span></span>
* <span data-ttu-id="a2143-170">Имя шлюза: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="a2143-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="a2143-171">Общедоступный IP-адрес: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="a2143-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="a2143-172">Тип VPN: RouteBased</span><span class="sxs-lookup"><span data-stu-id="a2143-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="a2143-173">Подключение: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="a2143-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="a2143-174">Тип подключения: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="a2143-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="a2143-175"><a name="Connect"></a>Шаг 1 — подключить tooyour подписки</span><span class="sxs-lookup"><span data-stu-id="a2143-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="a2143-176"><a name="TestVNet1"></a>Шаг 2. Создание и настройка TestVNet1</span><span class="sxs-lookup"><span data-stu-id="a2143-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="a2143-177">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a2143-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="a2143-178">Создание подсети TestVNet1 и hello для TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a2143-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="a2143-179">Пример ниже создает виртуальная сеть TestVNet1 и подсеть FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="a2143-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="a2143-180">Создание дополнительных адресного пространства для подсети hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a2143-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="a2143-181">Обратите внимание, что на этом шаге мы задать оба hello адресное пространство, которая была создана ранее, дополнительное адресное пространство, что мы хотим tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="a2143-182">Это обусловлено hello [обновления виртуальной сети сети az](https://docs.microsoft.com/cli/azure/network/vnet#update) команда перезаписывает предыдущие параметры hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="a2143-183">Убедитесь, что toospecify все префиксов адресов hello при использовании этой команды.</span><span class="sxs-lookup"><span data-stu-id="a2143-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="a2143-184">Создайте подсеть hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a2143-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="a2143-185">Создайте подсеть шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-185">Create hello gateway subnet.</span></span> <span data-ttu-id="a2143-186">Обратите внимание, что в этой подсети шлюза hello с именем «GatewaySubnet».</span><span class="sxs-lookup"><span data-stu-id="a2143-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="a2143-187">Это обязательное имя.</span><span class="sxs-lookup"><span data-stu-id="a2143-187">This name is required.</span></span> <span data-ttu-id="a2143-188">В этом примере hello подсеть шлюза используется /27.</span><span class="sxs-lookup"><span data-stu-id="a2143-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="a2143-189">Хотя возможных toocreate как /29 подсеть шлюза, рекомендуется создать подсеть большего размера, включающий несколько адресов, выбрав по крайней мере /28 или /27.</span><span class="sxs-lookup"><span data-stu-id="a2143-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="a2143-190">Это позволит достаточно адреса tooaccommodate возможные дополнительные настройки, вы можете в hello будущих.</span><span class="sxs-lookup"><span data-stu-id="a2143-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="a2143-191">Запрос открытый IP-адрес toobe toohello выделенный шлюз, создаваемых для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a2143-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="a2143-192">Обратите внимание, что hello AllocationMethod является динамической.</span><span class="sxs-lookup"><span data-stu-id="a2143-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="a2143-193">Нельзя указать hello IP-адреса, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="a2143-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="a2143-194">Он служит шлюзом динамически выделяемый tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2143-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="a2143-195">Создание шлюза виртуальной сети hello для TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a2143-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="a2143-196">Для подключений типа VNet-to-VNet необходимо использовать тип VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="a2143-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="a2143-197">При выполнении этой команды, с помощью hello параметр «--no - wait», вы не видите любой отзыв или выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a2143-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="a2143-198">Hello параметр «--no - wait» позволяет toocreate шлюза hello в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="a2143-199">Это не означает шлюза VPN hello завершает создание немедленно.</span><span class="sxs-lookup"><span data-stu-id="a2143-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="a2143-200">Создание шлюза часто занимает 45 минут или более, в зависимости от шлюза hello SKU, вы используете.</span><span class="sxs-lookup"><span data-stu-id="a2143-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="a2143-201"><a name="TestVNet4"></a>Шаг 3. Создание и настройка TestVNet4</span><span class="sxs-lookup"><span data-stu-id="a2143-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="a2143-202">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a2143-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="a2143-203">Создайте TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="a2143-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="a2143-204">Создайте дополнительную подсеть для TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="a2143-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="a2143-205">Создайте подсеть шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="a2143-206">Запросите общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a2143-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="a2143-207">Создание шлюза виртуальной сети TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="a2143-208"><a name="createconnect"></a>Шаг 4 — Создание подключений hello</span><span class="sxs-lookup"><span data-stu-id="a2143-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="a2143-209">Теперь у вас есть две виртуальные сети с VPN-шлюзами.</span><span class="sxs-lookup"><span data-stu-id="a2143-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="a2143-210">Hello следующим шагом является toocreate подключения через шлюз VPN между шлюзами виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="a2143-211">При использовании выше примерах hello шлюзов виртуальной сети находятся в разных группах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a2143-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="a2143-212">Когда шлюзы находятся в разных группах ресурсов, требуется tooidentify и укажите hello идентификаторы ресурсов для всех шлюзов, при установке соединения.</span><span class="sxs-lookup"><span data-stu-id="a2143-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="a2143-213">Если ваш виртуальных сетей в hello же группу ресурсов можно использовать hello [второй набор инструкций](#samerg) так, как идентификаторы ресурсов hello toospecify не требуется.</span><span class="sxs-lookup"><span data-stu-id="a2143-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="a2143-214"><a name="diffrg"></a>tooconnect виртуальных сетей, которые находятся в разных группах ресурсов</span><span class="sxs-lookup"><span data-stu-id="a2143-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="a2143-215">Получите идентификатор ресурса из VNet1GW hello из вывода hello hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a2143-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="a2143-216">В выходных данных hello найти hello «идентификатор:» строки.</span><span class="sxs-lookup"><span data-stu-id="a2143-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="a2143-217">Hello значения внутри кавычек hello, необходимые toocreate hello соединения в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="a2143-218">Скопируйте эти значения tooa текстовый редактор, например «Блокнот», чтобы их можно вставлять их при создании подключения.</span><span class="sxs-lookup"><span data-stu-id="a2143-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="a2143-219">Выходные данные примера:</span><span class="sxs-lookup"><span data-stu-id="a2143-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="a2143-220">Скопируйте значения hello после **«id»:** в кавычки hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="a2143-221">Получение hello VNet4GW из идентификатора ресурса и скопируйте hello значения tooa текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="a2143-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="a2143-222">Создание подключения tooTestVNet4 TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="a2143-223">На этом этапе можно создать подключение hello TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="a2143-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="a2143-224">Нет общего ключа, на который ссылается примеры hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="a2143-225">Можно использовать собственные значения для hello общего ключа.</span><span class="sxs-lookup"><span data-stu-id="a2143-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="a2143-226">Важно, что это общий ключ, hello Hello оба соединения должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="a2143-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="a2143-227">Создание подключения занимает некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a2143-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="a2143-228">Создание подключения tooTestVNet1 TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="a2143-229">Этот шаг является аналогичные toohello показано выше, за исключением того, вы создаете подключение hello из TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a2143-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="a2143-230">Убедитесь, что hello общие ключи совпадают.</span><span class="sxs-lookup"><span data-stu-id="a2143-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="a2143-231">Подключение hello tooestablish он занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a2143-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="a2143-232">Проверьте подключения.</span><span class="sxs-lookup"><span data-stu-id="a2143-232">Verify your connections.</span></span> <span data-ttu-id="a2143-233">Дополнительные сведения см. в разделе [Проверка подключений](#verify).</span><span class="sxs-lookup"><span data-stu-id="a2143-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="a2143-234"><a name="samerg"></a>tooconnect виртуальных сетей, в котором hello же группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="a2143-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="a2143-235">Создание подключения tooTestVNet4 TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="a2143-236">На этом этапе можно создать подключение hello TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="a2143-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="a2143-237">Группы ресурсов hello уведомления являются hello же в примерах hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="a2143-238">Появиться общий ключ, на который ссылается примеры hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="a2143-239">Однако hello общий ключ должен совпадать для обоих подключений, можно использовать собственные значения для hello общего ключа.</span><span class="sxs-lookup"><span data-stu-id="a2143-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="a2143-240">Создание подключения занимает некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a2143-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="a2143-241">Создание подключения tooTestVNet1 TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="a2143-242">Этот шаг является аналогичные toohello показано выше, за исключением того, вы создаете подключение hello из TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a2143-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="a2143-243">Убедитесь, что hello общие ключи совпадают.</span><span class="sxs-lookup"><span data-stu-id="a2143-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="a2143-244">Подключение hello tooestablish он занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a2143-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="a2143-245">Проверьте подключения.</span><span class="sxs-lookup"><span data-stu-id="a2143-245">Verify your connections.</span></span> <span data-ttu-id="a2143-246">Дополнительные сведения см. в разделе [Проверка подключений](#verify).</span><span class="sxs-lookup"><span data-stu-id="a2143-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="a2143-247"><a name="difsub"></a>Подключение виртуальных сетей из разных подписок</span><span class="sxs-lookup"><span data-stu-id="a2143-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![Схема подключения между виртуальными сетями](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="a2143-249">В этом сценарии мы создадим подключение между TestVNet1 и TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a2143-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="a2143-250">Hello виртуальных сетей находятся в разных подписках.</span><span class="sxs-lookup"><span data-stu-id="a2143-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="a2143-251">Hello подписки не обязательно toobe, связанный с hello того же клиента Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a2143-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="a2143-252">Hello этапах данной конфигурации добавьте дополнительное подключение виртуальной сети для виртуальной сети в порядке tooconnect TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a2143-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="a2143-253"><a name="TestVNet1diff"></a>Шаг 5. Создание и настройка TestVNet1</span><span class="sxs-lookup"><span data-stu-id="a2143-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="a2143-254">Эти инструкции по-прежнему из шагов hello в предыдущих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="a2143-255">Необходимо выполнить [шаг 1](#Connect) и [шаг 2](#TestVNet1) toocreate hello VPN-шлюза для TestVNet1 и настроите TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a2143-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="a2143-256">Для этой конфигурации не требуется toocreate TestVNet4 hello в предыдущем разделе, несмотря на то, что при ее создании, оно не будет конфликтовать с следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a2143-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="a2143-257">Выполнив шаг 1 и 2, перейдите к шагу 6.</span><span class="sxs-lookup"><span data-stu-id="a2143-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="a2143-258"><a name="verifyranges"></a>Шаг 6 - проверка hello диапазоны IP-адресов</span><span class="sxs-lookup"><span data-stu-id="a2143-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="a2143-259">При создании дополнительных подключений, это важно tooverify, пространство IP-адресов hello hello новой виртуальной сети не пересекается с любым из других диапазонов сети VNet или диапазоны шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="a2143-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="a2143-260">Для этого упражнения можно использовать следующие значения для hello TestVNet5 hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="a2143-261">**Значения для TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="a2143-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="a2143-262">Имя виртуальной сети: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="a2143-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="a2143-263">Группа ресурсов: TestRG5</span><span class="sxs-lookup"><span data-stu-id="a2143-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="a2143-264">Расположение: восточная часть Японии</span><span class="sxs-lookup"><span data-stu-id="a2143-264">Location: Japan East</span></span>
* <span data-ttu-id="a2143-265">TestVNet5: 10.51.0.0/16 и 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a2143-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="a2143-266">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a2143-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="a2143-267">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a2143-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="a2143-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="a2143-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="a2143-269">Имя шлюза: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="a2143-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="a2143-270">Общедоступный IP-адрес: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="a2143-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="a2143-271">Тип VPN: RouteBased</span><span class="sxs-lookup"><span data-stu-id="a2143-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="a2143-272">Подключение: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="a2143-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="a2143-273">Тип подключения: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="a2143-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="a2143-274"><a name="TestVNet5"></a>Шаг 7. Создание и настройка TestVNet5</span><span class="sxs-lookup"><span data-stu-id="a2143-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="a2143-275">Этот шаг необходимо выполнить в контексте hello hello новую подписку, 5 подписки.</span><span class="sxs-lookup"><span data-stu-id="a2143-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="a2143-276">Эта часть может выполняться Здравствуйте, администратор в другой организации, которой принадлежит подписка hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="a2143-277">tooswitch между подписками пользуются "az список учетных записей — все" toolist hello учетной записи tooyour доступные подписки, а затем "az учетная запись набора--подписки <subscriptionID>" tooswitch toohello подписки, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="a2143-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="a2143-278">Убедитесь, что вы подключенных tooSubscription 5, а затем создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a2143-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="a2143-279">Создайте TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a2143-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="a2143-280">Добавьте подсети.</span><span class="sxs-lookup"><span data-stu-id="a2143-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="a2143-281">Добавьте подсеть шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="a2143-282">Запросите общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a2143-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="a2143-283">Создание шлюза TestVNet5 hello</span><span class="sxs-lookup"><span data-stu-id="a2143-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="a2143-284"><a name="connections5"></a>Шаг 8 — Создание подключений hello</span><span class="sxs-lookup"><span data-stu-id="a2143-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="a2143-285">Мы разбить этот шаг в двух сеансах CLI, помеченные как **[подписки 1]**, и **[подписки 5]** так, как шлюзы hello находятся в разных подписках hello.</span><span class="sxs-lookup"><span data-stu-id="a2143-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="a2143-286">tooswitch между подписками пользуются "az список учетных записей — все" toolist hello учетной записи tooyour доступные подписки, а затем "az учетная запись набора--подписки <subscriptionID>" tooswitch toohello подписки, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="a2143-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="a2143-287">**[Подписки 1]**  Вход и подключиться tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="a2143-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="a2143-288">Выполнения hello следующая команда tooget hello имя и идентификатор hello шлюза hello в выходных данных:</span><span class="sxs-lookup"><span data-stu-id="a2143-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="a2143-289">Копировать выходные данные hello для «идентификатор:».</span><span class="sxs-lookup"><span data-stu-id="a2143-289">Copy hello output for "id:".</span></span> <span data-ttu-id="a2143-290">Отправьте hello идентификатор и имя hello hello виртуальной сети (VNet1GW) toohello администратор шлюза 5 подписки по электронной почте или другим методом.</span><span class="sxs-lookup"><span data-stu-id="a2143-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="a2143-291">Выходные данные примера:</span><span class="sxs-lookup"><span data-stu-id="a2143-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="a2143-292">**[Подписки 5]**  Вход и подключиться tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="a2143-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="a2143-293">Выполнения hello следующая команда tooget hello имя и идентификатор hello шлюза hello в выходных данных:</span><span class="sxs-lookup"><span data-stu-id="a2143-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="a2143-294">Копировать выходные данные hello для «идентификатор:».</span><span class="sxs-lookup"><span data-stu-id="a2143-294">Copy hello output for "id:".</span></span> <span data-ttu-id="a2143-295">Отправьте hello идентификатор и имя hello hello виртуальной сети (VNet5GW) toohello администратор шлюза 1 подписки по электронной почте или другим методом.</span><span class="sxs-lookup"><span data-stu-id="a2143-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="a2143-296">**[Подписки 1]**  На этом шаге создания hello подключения из TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a2143-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="a2143-297">Однако hello общий ключ должен совпадать для обоих подключений, можно использовать собственные значения для hello общего ключа.</span><span class="sxs-lookup"><span data-stu-id="a2143-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="a2143-298">Создание соединения может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a2143-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="a2143-299">Убедитесь, что подключение tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="a2143-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="a2143-300">**[Подписки 5]**  Этот шаг является аналогичные toohello показано выше, за исключением того, вы создаете подключение hello из TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a2143-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="a2143-301">Убедитесь, что hello общие ключи совпадают, а также подключение tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="a2143-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="a2143-302"><a name="verify"></a>Проверка подключений hello</span><span class="sxs-lookup"><span data-stu-id="a2143-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="a2143-303"><a name="faq"></a>Часто задаваемые вопросы о подключениях типа "виртуальная сеть — виртуальная сеть"</span><span class="sxs-lookup"><span data-stu-id="a2143-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a2143-304">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2143-304">Next steps</span></span>

* <span data-ttu-id="a2143-305">После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="a2143-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="a2143-306">Дополнительные сведения см. в разделе hello [документация по виртуальным машинам](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="a2143-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="a2143-307">Сведения о BGP см. в разделе hello [Обзор BGP](vpn-gateway-bgp-overview.md) и [как tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a2143-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
