---
title: "Установка подключения между виртуальными сетями Azure с помощью PowerShell | Документация Майкрософт"
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
ms.openlocfilehash: 8c42c0046ccaa98c572134042fbbb7e883ef93c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="a0eba-103">Настройка подключения VPN-шлюза между виртуальными сетями с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0eba-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="a0eba-104">В этой статье показано, как создать подключение VPN-шлюза между виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="a0eba-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="a0eba-105">Виртуальные сети могут относиться к одному или разным регионам и к одной или разным подпискам.</span><span class="sxs-lookup"><span data-stu-id="a0eba-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="a0eba-106">При подключении виртуальных сетей из разных подписок подписки не обязательно должны быть связаны с одним и тем же клиентом Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a0eba-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="a0eba-107">Приведенные в этой статье инструкции относятся к модели развертывания с помощью Resource Manager и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0eba-107">The steps in this article apply to the Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="a0eba-108">Эту конфигурацию также можно создать с помощью разных средств или моделей развертывания, выбрав вариант из следующего списка:</span><span class="sxs-lookup"><span data-stu-id="a0eba-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0eba-109">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="a0eba-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="a0eba-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0eba-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="a0eba-111">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="a0eba-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="a0eba-112">Портал Azure (классический)</span><span class="sxs-lookup"><span data-stu-id="a0eba-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="a0eba-113">Подключение с использованием разных моделей развертывания — портал Azure</span><span class="sxs-lookup"><span data-stu-id="a0eba-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="a0eba-114">Подключение с использованием разных моделей развертывания — PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0eba-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="a0eba-115">Подключение типа "виртуальная сеть — виртуальная сеть" похоже на подключение виртуальной сети к локальному сайту.</span><span class="sxs-lookup"><span data-stu-id="a0eba-115">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="a0eba-116">В обоих типах подключений используется VPN-шлюз для создания защищенного туннеля, использующего IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="a0eba-116">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="a0eba-117">Если виртуальные сети находятся в одном регионе, их можно соединить между собой с помощью пиринга.</span><span class="sxs-lookup"><span data-stu-id="a0eba-117">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="a0eba-118">При пиринговой связи между виртуальными сетями VPN-шлюз не используется.</span><span class="sxs-lookup"><span data-stu-id="a0eba-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="a0eba-119">Дополнительную информацию см. в статье [Пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0eba-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="a0eba-120">Подключение типа "виртуальная сеть — виртуальная сеть" можно комбинировать с многосайтовыми конфигурациями.</span><span class="sxs-lookup"><span data-stu-id="a0eba-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="a0eba-121">Это позволяет устанавливать топологии сети, совмещающие распределенные подключения с подключениями между виртуальными сетями, как показано на схеме ниже.</span><span class="sxs-lookup"><span data-stu-id="a0eba-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![Сведения о подключениях](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="a0eba-123">Что может дать связь между виртуальными сетями</span><span class="sxs-lookup"><span data-stu-id="a0eba-123">Why connect virtual networks?</span></span>

<span data-ttu-id="a0eba-124">Вам может потребоваться подключить виртуальные сети по следующим причинам.</span><span class="sxs-lookup"><span data-stu-id="a0eba-124">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="a0eba-125">**Межрегиональная географическая избыточность и географическое присутствие**</span><span class="sxs-lookup"><span data-stu-id="a0eba-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="a0eba-126">Вы можете настроить собственную георепликацию или синхронизацию с безопасной связью без прохождения трафика через конечные точки с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="a0eba-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="a0eba-127">С помощью Azure Load Balancer и диспетчера трафика можно настроить высокодоступную рабочую нагрузку с геоизбыточностью в нескольких регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="a0eba-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="a0eba-128">Одним из важных примеров является настройка SQL Always On с группами доступности, распределенными между несколькими регионами Azure.</span><span class="sxs-lookup"><span data-stu-id="a0eba-128">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="a0eba-129">**Региональные многоуровневые приложения с изоляцией или административной границей**</span><span class="sxs-lookup"><span data-stu-id="a0eba-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="a0eba-130">В одном регионе можно настроить многоуровневые приложения с несколькими виртуальными сетями, которые связаны друг с другом из-за требований к изоляции или административных требований.</span><span class="sxs-lookup"><span data-stu-id="a0eba-130">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="a0eba-131">Дополнительные сведения о подключениях типа "виртуальная сеть — виртуальная сеть" см. в разделе [Часто задаваемые вопросы о подключениях типа "виртуальная сеть — виртуальная сеть"](#faq) в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="a0eba-131">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="a0eba-132">Каким инструкциям следовать?</span><span class="sxs-lookup"><span data-stu-id="a0eba-132">Which set of steps should I use?</span></span>

<span data-ttu-id="a0eba-133">В этой статье приведены два разных набора действий.</span><span class="sxs-lookup"><span data-stu-id="a0eba-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="a0eba-134">Один предназначен для [виртуальных сетей в рамках одной подписки](#samesub), а другой — для [виртуальных сетей в разных подписках](#difsub).</span><span class="sxs-lookup"><span data-stu-id="a0eba-134">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="a0eba-135">Основные различия между этими наборами действий зависят от того, можно ли создать и настроить все ресурсы шлюза и виртуальной сети в ходе одного сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0eba-135">The key difference between the sets is whether you can create and configure all virtual network and gateway resources within the same PowerShell session.</span></span>

<span data-ttu-id="a0eba-136">В описанных ниже действиях используются переменные, объявляемые в начале каждого раздела.</span><span class="sxs-lookup"><span data-stu-id="a0eba-136">The steps in this article use variables that are declared at the beginning of each section.</span></span> <span data-ttu-id="a0eba-137">Если вы уже работаете с существующими виртуальными сетями, измените переменные в соответствии с параметрами своей среды.</span><span class="sxs-lookup"><span data-stu-id="a0eba-137">If you already are working with existing VNets, modify the variables to reflect the settings in your own environment.</span></span> <span data-ttu-id="a0eba-138">Сведения о разрешении имен виртуальных машин см. в [этой статье](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="a0eba-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="a0eba-139"><a name="samesub"></a>Подключение виртуальных сетей из одной подписки</span><span class="sxs-lookup"><span data-stu-id="a0eba-139"><a name="samesub"></a>How to connect VNets that are in the same subscription</span></span>

![Схема подключения между виртуальными сетями](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="a0eba-141">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a0eba-141">Before you begin</span></span>

<span data-ttu-id="a0eba-142">Прежде всего вам необходимо установить последнюю версию командлетов PowerShell для Azure Resource Manager (4.0 или более позднюю).</span><span class="sxs-lookup"><span data-stu-id="a0eba-142">Before beginning, you need to install the latest version of the Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="a0eba-143">См. дополнительные сведения об [установке и настройке командлетов Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a0eba-143">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="a0eba-144"><a name="Step1"></a>Шаг 1. Планирование диапазонов IP-адресов</span><span class="sxs-lookup"><span data-stu-id="a0eba-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="a0eba-145">Далее мы создадим две виртуальные сети с соответствующими шлюзами и конфигурациями подсетей.</span><span class="sxs-lookup"><span data-stu-id="a0eba-145">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="a0eba-146">Затем мы создадим VPN-подключение между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="a0eba-146">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="a0eba-147">В конфигурации сети важно задать диапазоны IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a0eba-147">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="a0eba-148">Имейте в виду, необходимо убедиться в том, что ни один из диапазонов виртуальных сетей или диапазонов локальных сетей никак не перекрываются.</span><span class="sxs-lookup"><span data-stu-id="a0eba-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="a0eba-149">В этих примерах мы не включаем DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="a0eba-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="a0eba-150">Сведения о разрешении имен виртуальных машин см. в [этой статье](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="a0eba-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="a0eba-151">В примерах мы используем следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a0eba-151">We use the following values in the examples:</span></span>

<span data-ttu-id="a0eba-152">**Значения для TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="a0eba-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="a0eba-153">Имя виртуальной сети: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="a0eba-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="a0eba-154">Группа ресурсов: TestRG1</span><span class="sxs-lookup"><span data-stu-id="a0eba-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="a0eba-155">Расположение: восточная часть США</span><span class="sxs-lookup"><span data-stu-id="a0eba-155">Location: East US</span></span>
* <span data-ttu-id="a0eba-156">TestVNet1: 10.11.0.0/16 и 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a0eba-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="a0eba-157">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a0eba-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="a0eba-158">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a0eba-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="a0eba-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="a0eba-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="a0eba-160">Имя шлюза: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="a0eba-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="a0eba-161">Общедоступный IP-адрес: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="a0eba-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="a0eba-162">Тип VPN: RouteBased</span><span class="sxs-lookup"><span data-stu-id="a0eba-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="a0eba-163">Подключение (1–4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="a0eba-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="a0eba-164">Подключение (1–5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="a0eba-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="a0eba-165">Тип подключения: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="a0eba-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="a0eba-166">**Значения для TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="a0eba-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="a0eba-167">Имя виртуальной сети: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="a0eba-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="a0eba-168">TestVNet2: 10.41.0.0/16 и 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a0eba-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="a0eba-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a0eba-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="a0eba-170">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a0eba-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="a0eba-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="a0eba-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="a0eba-172">Группа ресурсов: TestRG4</span><span class="sxs-lookup"><span data-stu-id="a0eba-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="a0eba-173">Расположение: Запад США</span><span class="sxs-lookup"><span data-stu-id="a0eba-173">Location: West US</span></span>
* <span data-ttu-id="a0eba-174">Имя шлюза: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="a0eba-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="a0eba-175">Общедоступный IP-адрес: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="a0eba-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="a0eba-176">Тип VPN: RouteBased</span><span class="sxs-lookup"><span data-stu-id="a0eba-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="a0eba-177">Подключение: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="a0eba-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="a0eba-178">Тип подключения: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="a0eba-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="a0eba-179"><a name="Step2"></a>Шаг 2. Создание и настройка TestVNet1</span><span class="sxs-lookup"><span data-stu-id="a0eba-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="a0eba-180">Объявите переменные.</span><span class="sxs-lookup"><span data-stu-id="a0eba-180">Declare your variables.</span></span> <span data-ttu-id="a0eba-181">В этом примере объявлены переменные со значениями для этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="a0eba-181">This example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="a0eba-182">В большинстве случаев эти значения вам нужно заменить собственными.</span><span class="sxs-lookup"><span data-stu-id="a0eba-182">In most cases, you should replace the values with your own.</span></span> <span data-ttu-id="a0eba-183">Но вы можете использовать указанные переменные, чтобы ознакомиться с этим типом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a0eba-183">However, you can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="a0eba-184">Измените переменные (при необходимости), а затем скопируйте и вставьте их в консоль PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0eba-184">Modify the variables if needed, then copy and paste them into your PowerShell console.</span></span>

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

2. <span data-ttu-id="a0eba-185">Подключитесь к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a0eba-185">Connect to your account.</span></span> <span data-ttu-id="a0eba-186">Для подключения используйте следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="a0eba-186">Use the following example to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="a0eba-187">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a0eba-187">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="a0eba-188">Укажите подписку, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="a0eba-188">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="a0eba-189">Создайте новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a0eba-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="a0eba-190">Создайте конфигурации подсети для TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a0eba-190">Create the subnet configurations for TestVNet1.</span></span> <span data-ttu-id="a0eba-191">В этом примере создается виртуальная сеть с именем TestVNet1 и три подсети: GatewaySubnet, FrontEnd и Backend.</span><span class="sxs-lookup"><span data-stu-id="a0eba-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="a0eba-192">При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="a0eba-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="a0eba-193">Если вы используете другое имя, создание шлюза завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="a0eba-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="a0eba-194">В следующем примере используются переменные, заданные ранее.</span><span class="sxs-lookup"><span data-stu-id="a0eba-194">The following example uses the variables that you set earlier.</span></span> <span data-ttu-id="a0eba-195">В этом примере в подсети шлюза используется длина префикса /27.</span><span class="sxs-lookup"><span data-stu-id="a0eba-195">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="a0eba-196">Хотя можно создать подсеть шлюза размером /29, рекомендуется создать подсеть большего размера, включающую несколько адресов, выбрав по крайней мере значение /28 или /27.</span><span class="sxs-lookup"><span data-stu-id="a0eba-196">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="a0eba-197">Таким образом, у вас будет достаточно адресов, чтобы добавить дополнительные конфигурации в будущем.</span><span class="sxs-lookup"><span data-stu-id="a0eba-197">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="a0eba-198">Создайте TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a0eba-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="a0eba-199">Запросите выделение общедоступного IP-адреса для шлюза, который будет создан для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a0eba-199">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="a0eba-200">Учтите, что параметр AllocationMethod является динамическим.</span><span class="sxs-lookup"><span data-stu-id="a0eba-200">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="a0eba-201">Указать необходимый IP-адрес нельзя.</span><span class="sxs-lookup"><span data-stu-id="a0eba-201">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="a0eba-202">Он выделяется для шлюза динамически.</span><span class="sxs-lookup"><span data-stu-id="a0eba-202">It's dynamically allocated to your gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="a0eba-203">Создайте конфигурацию шлюза.</span><span class="sxs-lookup"><span data-stu-id="a0eba-203">Create the gateway configuration.</span></span> <span data-ttu-id="a0eba-204">Конфигурация шлюза определяет используемые подсеть и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a0eba-204">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="a0eba-205">Используйте следующий пример, чтобы создать конфигурацию шлюза.</span><span class="sxs-lookup"><span data-stu-id="a0eba-205">Use the example to create your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="a0eba-206">Создайте шлюз для TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a0eba-206">Create the gateway for TestVNet1.</span></span> <span data-ttu-id="a0eba-207">На этом шаге вы создадите шлюз для виртуальной сети TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a0eba-207">In this step, you create the virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="a0eba-208">Для подключений типа VNet-to-VNet необходимо использовать тип VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="a0eba-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="a0eba-209">Создание шлюза часто занимает 45 минут и более, в зависимости от выбранного SKU шлюза.</span><span class="sxs-lookup"><span data-stu-id="a0eba-209">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="a0eba-210">Шаг 3. Создание и настройка TestVNet4</span><span class="sxs-lookup"><span data-stu-id="a0eba-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="a0eba-211">После настройки TestVNet1 создайте TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="a0eba-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="a0eba-212">Следуйте инструкциям ниже, заменив при необходимости значения своими.</span><span class="sxs-lookup"><span data-stu-id="a0eba-212">Follow the steps below, replacing the values with your own when needed.</span></span> <span data-ttu-id="a0eba-213">Этот шаг можно выполнять в том же сеансе PowerShell, так как мы работаем в той же подписке.</span><span class="sxs-lookup"><span data-stu-id="a0eba-213">This step can be done within the same PowerShell session because it is in the same subscription.</span></span>

1. <span data-ttu-id="a0eba-214">Объявите переменные.</span><span class="sxs-lookup"><span data-stu-id="a0eba-214">Declare your variables.</span></span> <span data-ttu-id="a0eba-215">Не забудьте заменить значения теми, которые вы хотите использовать для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a0eba-215">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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
2. <span data-ttu-id="a0eba-216">Создайте новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a0eba-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="a0eba-217">Создайте конфигурации подсети для TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="a0eba-217">Create the subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="a0eba-218">Создайте TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="a0eba-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="a0eba-219">Запросите общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a0eba-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="a0eba-220">Создайте конфигурацию шлюза.</span><span class="sxs-lookup"><span data-stu-id="a0eba-220">Create the gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="a0eba-221">Создание шлюза TestVNet4</span><span class="sxs-lookup"><span data-stu-id="a0eba-221">Create the TestVNet4 gateway.</span></span> <span data-ttu-id="a0eba-222">Создание шлюза часто занимает 45 минут и более, в зависимости от выбранного SKU шлюза.</span><span class="sxs-lookup"><span data-stu-id="a0eba-222">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-the-connections"></a><span data-ttu-id="a0eba-223">Шаг 4. Создание подключений</span><span class="sxs-lookup"><span data-stu-id="a0eba-223">Step 4 - Create the connections</span></span>

1. <span data-ttu-id="a0eba-224">Получите оба шлюза для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="a0eba-224">Get both virtual network gateways.</span></span> <span data-ttu-id="a0eba-225">Если оба шлюза находятся в одной подписке, как в этом примере, этот шаг можно выполнить в одном сеансе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0eba-225">If both of the gateways are in the same subscription, as they are in the example, you can complete this step in the same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="a0eba-226">Создайте подключение между TestVNet1 и TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="a0eba-226">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="a0eba-227">На этом шаге вы создадите подключение между TestVNet1 и TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="a0eba-227">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="a0eba-228">Вы увидите ссылки на общий ключ в примерах.</span><span class="sxs-lookup"><span data-stu-id="a0eba-228">You'll see a shared key referenced in the examples.</span></span> <span data-ttu-id="a0eba-229">Можно использовать собственные значения для общего ключа.</span><span class="sxs-lookup"><span data-stu-id="a0eba-229">You can use your own values for the shared key.</span></span> <span data-ttu-id="a0eba-230">Важно, чтобы общий ключ в обоих подключениях был одинаковым.</span><span class="sxs-lookup"><span data-stu-id="a0eba-230">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="a0eba-231">Создание подключения может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="a0eba-231">Creating a connection can take a short while to complete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="a0eba-232">Создайте подключение между TestVNet4 и TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a0eba-232">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="a0eba-233">Этот шаг аналогичен приведенному выше, за исключением того, что создается подключение из сети TestVNet4 в сеть TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a0eba-233">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="a0eba-234">Убедитесь, что общие ключи совпадают.</span><span class="sxs-lookup"><span data-stu-id="a0eba-234">Make sure the shared keys match.</span></span> <span data-ttu-id="a0eba-235">Подключение установится через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a0eba-235">The connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="a0eba-236">Проверьте подключение.</span><span class="sxs-lookup"><span data-stu-id="a0eba-236">Verify your connection.</span></span> <span data-ttu-id="a0eba-237">См. раздел о [проверке подключения](#verify).</span><span class="sxs-lookup"><span data-stu-id="a0eba-237">See the section [How to verify your connection](#verify).</span></span>

## <span data-ttu-id="a0eba-238"><a name="difsub"></a>Подключение виртуальных сетей из разных подписок</span><span class="sxs-lookup"><span data-stu-id="a0eba-238"><a name="difsub"></a>How to connect VNets that are in different subscriptions</span></span>

![Схема подключения между виртуальными сетями](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="a0eba-240">В этом сценарии мы создадим подключение между TestVNet1 и TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a0eba-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="a0eba-241">TestVNet1 и TestVNet5 находятся в разных подписках.</span><span class="sxs-lookup"><span data-stu-id="a0eba-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="a0eba-242">Подписки не обязательно должны быть связаны с одним и тем же клиентом Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a0eba-242">The subscriptions do not need to be associated with the same Active Directory tenant.</span></span> <span data-ttu-id="a0eba-243">Разница между этими действиями и предыдущими заключается в том, что часть настройки нужно выполнить в отдельном сеансе PowerShell в контексте второй подписки,</span><span class="sxs-lookup"><span data-stu-id="a0eba-243">The difference between these steps and the previous set is that some of the configuration steps need to be performed in a separate PowerShell session in the context of the second subscription.</span></span> <span data-ttu-id="a0eba-244">особенно если две подписки используются разными организациями.</span><span class="sxs-lookup"><span data-stu-id="a0eba-244">Especially when the two subscriptions belong to different organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="a0eba-245">Шаг 5. Создание и настройка TestVNet1</span><span class="sxs-lookup"><span data-stu-id="a0eba-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="a0eba-246">Чтобы создать и настроить сеть TestVNet1 и VPN-шлюз для нее, необходимо выполнить [шаг 1](#Step1) и [шаг 2](#Step2) из предыдущего раздела.</span><span class="sxs-lookup"><span data-stu-id="a0eba-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from the previous section to create and configure TestVNet1 and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="a0eba-247">В этой конфигурации не нужно создавать TestVNet4 из предыдущего раздела. Но если вы создадите эту виртуальную сеть, она не помешает при выполнении этих шагов.</span><span class="sxs-lookup"><span data-stu-id="a0eba-247">For this configuration, you are not required to create TestVNet4 from the previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="a0eba-248">Выполнив шаг 1 и 2, перейдите к шагу 6, чтобы создать сеть TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a0eba-248">Once you complete Step 1 and Step 2, continue with Step 6 to create TestVNet5.</span></span> 

### <a name="step-6---verify-the-ip-address-ranges"></a><span data-ttu-id="a0eba-249">Шаг 6. Проверка диапазонов IP-адресов</span><span class="sxs-lookup"><span data-stu-id="a0eba-249">Step 6 - Verify the IP address ranges</span></span>

<span data-ttu-id="a0eba-250">Важно проследить, чтобы пространство IP-адресов для новой виртуальной сети TestVNet5 не пересекалось с диапазонами других виртуальных сетей или диапазонами шлюзов локальной сети.</span><span class="sxs-lookup"><span data-stu-id="a0eba-250">It is important to make sure that the IP address space of the new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="a0eba-251">В этом примере виртуальные сети могут принадлежать разным организациям.</span><span class="sxs-lookup"><span data-stu-id="a0eba-251">In this example, the virtual networks may belong to different organizations.</span></span> <span data-ttu-id="a0eba-252">В этом упражнении используйте следующие значения для сети TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a0eba-252">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="a0eba-253">**Значения для TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="a0eba-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="a0eba-254">Имя виртуальной сети: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="a0eba-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="a0eba-255">Группа ресурсов: TestRG5</span><span class="sxs-lookup"><span data-stu-id="a0eba-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="a0eba-256">Расположение: восточная часть Японии</span><span class="sxs-lookup"><span data-stu-id="a0eba-256">Location: Japan East</span></span>
* <span data-ttu-id="a0eba-257">TestVNet5: 10.51.0.0/16 и 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a0eba-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="a0eba-258">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a0eba-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="a0eba-259">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a0eba-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="a0eba-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="a0eba-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="a0eba-261">Имя шлюза: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="a0eba-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="a0eba-262">Общедоступный IP-адрес: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="a0eba-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="a0eba-263">Тип VPN: RouteBased</span><span class="sxs-lookup"><span data-stu-id="a0eba-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="a0eba-264">Подключение: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="a0eba-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="a0eba-265">Тип подключения: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="a0eba-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="a0eba-266">Шаг 7. Создание и настройка TestVNet5</span><span class="sxs-lookup"><span data-stu-id="a0eba-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="a0eba-267">Это действие необходимо выполнить в контексте новой подписки.</span><span class="sxs-lookup"><span data-stu-id="a0eba-267">This step must be done in the context of the new subscription.</span></span> <span data-ttu-id="a0eba-268">Эту часть может выполнить администратор в другой организации, которой принадлежит подписка.</span><span class="sxs-lookup"><span data-stu-id="a0eba-268">This part may be performed by the administrator in a different organization that owns the subscription.</span></span>

1. <span data-ttu-id="a0eba-269">Объявите переменные.</span><span class="sxs-lookup"><span data-stu-id="a0eba-269">Declare your variables.</span></span> <span data-ttu-id="a0eba-270">Не забудьте заменить значения теми, которые вы хотите использовать для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a0eba-270">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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
2. <span data-ttu-id="a0eba-271">Подключитесь к подписке 5.</span><span class="sxs-lookup"><span data-stu-id="a0eba-271">Connect to subscription 5.</span></span> <span data-ttu-id="a0eba-272">Откройте консоль PowerShell и подключитесь к своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a0eba-272">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="a0eba-273">Для подключения используйте следующий пример.</span><span class="sxs-lookup"><span data-stu-id="a0eba-273">Use the following sample to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="a0eba-274">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a0eba-274">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="a0eba-275">Укажите подписку, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="a0eba-275">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="a0eba-276">Создайте новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a0eba-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="a0eba-277">Создайте конфигурации подсети для TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a0eba-277">Create the subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="a0eba-278">Создайте TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a0eba-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="a0eba-279">Запросите общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a0eba-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="a0eba-280">Создайте конфигурацию шлюза.</span><span class="sxs-lookup"><span data-stu-id="a0eba-280">Create the gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="a0eba-281">Создайте шлюз TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a0eba-281">Create the TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-the-connections"></a><span data-ttu-id="a0eba-282">Шаг 8. Создание подключений</span><span class="sxs-lookup"><span data-stu-id="a0eba-282">Step 8 - Create the connections</span></span>

<span data-ttu-id="a0eba-283">Так как шлюзы из нашего примера находятся в разных подписках, мы разделили этот шаг на два сеанса PowerShell, обозначенные как [подписка 1] и [подписка 5].</span><span class="sxs-lookup"><span data-stu-id="a0eba-283">In this example, because the gateways are in the different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="a0eba-284">**[Подписка 1]**. Получите шлюз виртуальной сети для подписки 1</span><span class="sxs-lookup"><span data-stu-id="a0eba-284">**[Subscription 1]** Get the virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="a0eba-285">Войдите в систему и подключитесь к подписке 1, а затем выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a0eba-285">Log in and connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="a0eba-286">Скопируйте выходные данные следующих элементов и отправьте их администратору подписки 5 по электронной почте или другим способом.</span><span class="sxs-lookup"><span data-stu-id="a0eba-286">Copy the output of the following elements and send these to the administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="a0eba-287">Эти два элемента будут иметь значения, похожие на выходные данные в нашем примере:</span><span class="sxs-lookup"><span data-stu-id="a0eba-287">These two elements will have values similar to the following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="a0eba-288">**[Подписка 5]**. Получите шлюз виртуальной сети для подписки 5.</span><span class="sxs-lookup"><span data-stu-id="a0eba-288">**[Subscription 5]** Get the virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="a0eba-289">Войдите в систему и подключитесь к подписке 5, а затем выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a0eba-289">Log in and connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="a0eba-290">Скопируйте выходные данные следующих элементов и отправьте их администратору подписки 1 по электронной почте или другим способом.</span><span class="sxs-lookup"><span data-stu-id="a0eba-290">Copy the output of the following elements and send these to the administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="a0eba-291">Эти два элемента будут иметь значения, похожие на выходные данные в нашем примере:</span><span class="sxs-lookup"><span data-stu-id="a0eba-291">These two elements will have values similar to the following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="a0eba-292">**[Подписка 1]**. Создайте подключение между TestVNet1 и TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a0eba-292">**[Subscription 1]** Create the TestVNet1 to TestVNet5 connection.</span></span> <span data-ttu-id="a0eba-293">На этом шаге вы создадите подключение между TestVNet1 и TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="a0eba-293">In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="a0eba-294">Разница здесь заключается в том, что вы не можете напрямую получить $vnet5gw, так как это значение используется в другой подписке.</span><span class="sxs-lookup"><span data-stu-id="a0eba-294">The difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="a0eba-295">Вам необходимо создать новый объект PowerShell с помощью значений, переданных из подписки 1 на предыдущих этапах.</span><span class="sxs-lookup"><span data-stu-id="a0eba-295">You will need to create a new PowerShell object with the values communicated from Subscription 1 in the steps above.</span></span> <span data-ttu-id="a0eba-296">Используйте пример ниже.</span><span class="sxs-lookup"><span data-stu-id="a0eba-296">Use the example below.</span></span> <span data-ttu-id="a0eba-297">Замените имя, идентификатор и общий ключ своими значениями.</span><span class="sxs-lookup"><span data-stu-id="a0eba-297">Replace the Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="a0eba-298">Важно, чтобы общий ключ в обоих подключениях был одинаковым.</span><span class="sxs-lookup"><span data-stu-id="a0eba-298">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="a0eba-299">Создание подключения может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="a0eba-299">Creating a connection can take a short while to complete.</span></span>

  <span data-ttu-id="a0eba-300">Подключитесь к подписке 1, а затем выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a0eba-300">Connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="a0eba-301">**[Подписка 5]**. Создайте подключение между TestVNet5 и TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a0eba-301">**[Subscription 5]** Create the TestVNet5 to TestVNet1 connection.</span></span> <span data-ttu-id="a0eba-302">Этот шаг аналогичен приведенному выше, за исключением того, что создается подключение из сети TestVNet5 в сеть TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a0eba-302">This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="a0eba-303">На этом шаге процесс создания объекта PowerShell аналогичный, но с использованием значений, полученных из подписки 1.</span><span class="sxs-lookup"><span data-stu-id="a0eba-303">The same process of creating a PowerShell object based on the values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="a0eba-304">Проследите на этом шаге, чтобы общие ключи совпадали.</span><span class="sxs-lookup"><span data-stu-id="a0eba-304">In this step, be sure that the shared keys match.</span></span>

  <span data-ttu-id="a0eba-305">Подключитесь к подписке 5, а затем выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a0eba-305">Connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="a0eba-306"><a name="verify"></a>Проверка подключения</span><span class="sxs-lookup"><span data-stu-id="a0eba-306"><a name="verify"></a>How to verify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="a0eba-307"><a name="faq"></a>Часто задаваемые вопросы о подключениях типа "виртуальная сеть — виртуальная сеть"</span><span class="sxs-lookup"><span data-stu-id="a0eba-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a0eba-308">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a0eba-308">Next steps</span></span>

* <span data-ttu-id="a0eba-309">Установив подключение, можно добавить виртуальные машины в виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="a0eba-309">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="a0eba-310">Дополнительную информацию см. в [документации по виртуальным машинам](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="a0eba-310">See the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="a0eba-311">Сведения о BGP см. в статьях [Обзор использования BGP с VPN-шлюзами Azure](vpn-gateway-bgp-overview.md) и [Настройка BGP на VPN-шлюзах Azure с помощью Azure Resource Manager и PowerShell](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a0eba-311">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>