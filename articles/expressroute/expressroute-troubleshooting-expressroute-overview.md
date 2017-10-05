---
title: "Проверка подключения. Руководство по устранению неполадок Azure ExpressRoute | Документация Майкрософт"
description: "В этой статье содержатся инструкции по устранению неполадок и проверке сквозного подключения канала ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 5a6360b56963d219ab576fb3e2636b6c51dd72ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="07fea-103">Проверка подключения ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="07fea-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="07fea-104">Подключение ExpressRoute, расширяющее локальную сеть в Microsoft Cloud посредством частного подключения, которое обеспечивает поставщик услуг подключения, включает в себя следующие три различные сетевые зоны:</span><span class="sxs-lookup"><span data-stu-id="07fea-104">ExpressRoute, which extends an on-premises network into the Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves the following three distinct network zones:</span></span>

-   <span data-ttu-id="07fea-105">клиентскую сеть;</span><span class="sxs-lookup"><span data-stu-id="07fea-105">Customer Network</span></span>
-   <span data-ttu-id="07fea-106">сеть поставщика;</span><span class="sxs-lookup"><span data-stu-id="07fea-106">Provider Network</span></span>
-   <span data-ttu-id="07fea-107">центр обработки данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="07fea-107">Microsoft Datacenter</span></span>

<span data-ttu-id="07fea-108">Цель данного документа — помочь пользователю определить, где (при наличии) существует проблема с подключением и в какой зоне, чтобы устранить ее при помощи соответствующей группы поддержки.</span><span class="sxs-lookup"><span data-stu-id="07fea-108">The purpose of this document is to help user to identify where (or even if) a connectivity issue exists and within which zone, thereby to seek help from appropriate team to resolve the issue.</span></span> <span data-ttu-id="07fea-109">Если для устранения проблемы необходима помощь службы поддержки Майкрософт, отправьте запрос в [службу поддержки Майкрософт][Support].</span><span class="sxs-lookup"><span data-stu-id="07fea-109">If Microsoft support is needed to resolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07fea-110">Данный документ предназначен для диагностики и устранения простых проблем.</span><span class="sxs-lookup"><span data-stu-id="07fea-110">This document is intended to help diagnosing and fixing simple issues.</span></span> <span data-ttu-id="07fea-111">Он не заменит услуг службы поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="07fea-111">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="07fea-112">Если вам не удается устранить проблему, используя приведенные здесь рекомендации, то необходимо отправить запрос в [службу поддержки Майкрософт][Support].</span><span class="sxs-lookup"><span data-stu-id="07fea-112">Open a support ticket with [Microsoft Support][Support] if you are unable to solve the problem using the guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="07fea-113">Обзор</span><span class="sxs-lookup"><span data-stu-id="07fea-113">Overview</span></span>
<span data-ttu-id="07fea-114">На следующей схеме показано логическое подключение между клиентской сетью и сетью Майкрософт через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="07fea-114">The following diagram shows the logical connectivity of a customer network to Microsoft network using ExpressRoute.</span></span>
<span data-ttu-id="07fea-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="07fea-115">[![1]][1]</span></span>

<span data-ttu-id="07fea-116">На предыдущей схеме цифры обозначают ключевые точки сети.</span><span class="sxs-lookup"><span data-stu-id="07fea-116">In the preceding diagram, the numbers indicate key network points.</span></span> <span data-ttu-id="07fea-117">Для указания точек сети в этой статье часто используются номера.</span><span class="sxs-lookup"><span data-stu-id="07fea-117">The network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="07fea-118">В зависимости от модели подключения ExpressRoute (совместное размещение Cloud Exchange, Ethernet-подключение типа "точка — точка" или подключение типа "любой к любому" (IPVPN)) точки сети 3 и 4 могут быть коммутаторами (устройства уровня 2).</span><span class="sxs-lookup"><span data-stu-id="07fea-118">Depending on the ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) the network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="07fea-119">Ниже приведены представленные на схеме ключевые точки сети.</span><span class="sxs-lookup"><span data-stu-id="07fea-119">The key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="07fea-120">Клиентское вычислительное устройство (например, сервер или компьютер).</span><span class="sxs-lookup"><span data-stu-id="07fea-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="07fea-121">Клиентские пограничные маршрутизаторы (CE).</span><span class="sxs-lookup"><span data-stu-id="07fea-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="07fea-122">Пограничные маршрутизаторы (коммутаторы) поставщика услуг связи, подключенные к клиентским пограничным маршрутизаторам (PE, подключенные к CE).</span><span class="sxs-lookup"><span data-stu-id="07fea-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="07fea-123">В этом документе называются PE-CE.</span><span class="sxs-lookup"><span data-stu-id="07fea-123">Referred to as PE-CEs in this document.</span></span>
4.  <span data-ttu-id="07fea-124">Пограничные маршрутизаторы (коммутаторы) поставщика услуг связи, подключенные к MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="07fea-125">В этом документе называются PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-125">Referred to as PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="07fea-126">Маршрутизаторы MSEE ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="07fea-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="07fea-127">Шлюз виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="07fea-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="07fea-128">Вычислительное устройство в виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="07fea-128">Compute device on the Azure VNet</span></span>

<span data-ttu-id="07fea-129">При использовании моделей подключения "совместное размещение Cloud Exchange" или "Ethernet-подключение типа "точка — точка" клиентский пограничный маршрутизатор (2) устанавливает пиринг BGP с маршрутизаторами MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="07fea-129">If the Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, the customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="07fea-130">Точки сети 3 и 4 будут по-прежнему существовать, но будут в некоторой степени прозрачными как устройства уровня 2.</span><span class="sxs-lookup"><span data-stu-id="07fea-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="07fea-131">Если используется модель подключения типа "любой к любому" (IPVPN), маршрутизаторы PE (подключенные к MSEE) (4) устанавливают пиринг BGP с маршрутизаторами MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="07fea-131">If the Any-to-any (IPVPN) connectivity model is used, the PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="07fea-132">Затем маршруты будут распространяться в обратном направлении в сеть клиента по сети поставщика услуг IPVPN.</span><span class="sxs-lookup"><span data-stu-id="07fea-132">Routes would then propagate back to the customer network via the IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="07fea-133">Для обеспечения высокой доступности ExpressRoute корпорации Майкрософт необходима избыточная пара сеансов BGP между маршрутизаторами MSEE (5) и маршрутизаторами поставщика услуг связи, подключенными к MSEE (PE-MSEE) (4).</span><span class="sxs-lookup"><span data-stu-id="07fea-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="07fea-134">Рекомендуется также избыточная пара сетевых путей между клиентской сетью и маршрутизаторами PE-CE.</span><span class="sxs-lookup"><span data-stu-id="07fea-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="07fea-135">Однако в модели подключения типа "любой к любому" (IPVPN) одно устройство CE (2) может быть подключено к одному или нескольким маршрутизаторам PE (3).</span><span class="sxs-lookup"><span data-stu-id="07fea-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected to one or more PEs (3).</span></span>
>
>

<span data-ttu-id="07fea-136">Чтобы проверить канал ExpressRoute (точки сети обозначаются соответствующими номерами), необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="07fea-136">To validate an ExpressRoute circuit, the following steps are covered (with the network point indicated by the associated number):</span></span>
1. [<span data-ttu-id="07fea-137">Проверить подготовку и состояние канала (5).</span><span class="sxs-lookup"><span data-stu-id="07fea-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="07fea-138">Проверить, что настроен по крайней мере один пиринг ExpressRoute (5).</span><span class="sxs-lookup"><span data-stu-id="07fea-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="07fea-139">Проверить ARP между корпорацией Майкрософт и поставщиком услуг связи (соединение между точками 4 и 5).</span><span class="sxs-lookup"><span data-stu-id="07fea-139">Validate ARP between Microsoft and the service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="07fea-140">Проверить BGP и маршруты для MSEE (BGP между точками 4–5 и 5–6, если подключена виртуальная сеть).</span><span class="sxs-lookup"><span data-stu-id="07fea-140">Validate BGP and routes on the MSEE (BGP between 4 to 5, and 5 to 6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="07fea-141">Проверить статистику трафика (трафика, проходящего через точку 5).</span><span class="sxs-lookup"><span data-stu-id="07fea-141">Check the Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="07fea-142">Дополнительные проверки будут добавлены в будущем. Проверяйте ежемесячно!</span><span class="sxs-lookup"><span data-stu-id="07fea-142">More validations and checks will be added in the future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="07fea-143">Проверка подготовки и состояния канала</span><span class="sxs-lookup"><span data-stu-id="07fea-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="07fea-144">Независимо от модели подключения необходимо создать канал ExpressRoute и соответственно сгенерировать ключ службы для подготовки канала.</span><span class="sxs-lookup"><span data-stu-id="07fea-144">Regardless of the connectivity model, an ExpressRoute circuit has to be created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="07fea-145">При подготовке канала ExpressRoute устанавливаются избыточные подключения уровня 2 между маршрутизаторами PE-MSEE (4) и MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="07fea-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="07fea-146">Дополнительные сведения о создании, изменении, подготовке и проверке канала ExpressRoute см. в статье [Создание и изменение канала ExpressRoute][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="07fea-146">For more information on how to create, modify, provision, and verify an ExpressRoute circuit, see the article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="07fea-147">Ключ службы однозначно идентифицирует канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="07fea-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="07fea-148">Этот ключ необходим для большинства команд PowerShell, упомянутых в данном документе.</span><span class="sxs-lookup"><span data-stu-id="07fea-148">This key is required for most of the powershell commands mentioned in this document.</span></span> <span data-ttu-id="07fea-149">Если вам необходима помощь от корпорации Майкрософт или от партнера ExpressRoute в устранении неполадок с ExpressRoute, укажите ключ службы для оперативного определения канала.</span><span class="sxs-lookup"><span data-stu-id="07fea-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner to troubleshoot an ExpressRoute issue, provide the service key to readily identify the circuit.</span></span>
>
>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="07fea-150">Проверка на портале Azure</span><span class="sxs-lookup"><span data-stu-id="07fea-150">Verification via the Azure portal</span></span>
<span data-ttu-id="07fea-151">На портале Azure можно проверить состояние канала ExpressRoute, выбрав ![2][2] в боковом меню слева, а затем выбрав канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="07fea-151">In the Azure portal, the status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="07fea-152">Выберите канал ExpressRoute в разделе "Все ресурсы", после чего откроется колонка канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="07fea-152">Selecting an ExpressRoute circuit listed under "All resources" opens the ExpressRoute circuit blade.</span></span> <span data-ttu-id="07fea-153">В ![3][3] разделе колонки отображаются основные сведения об ExpressRoute, как показано на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="07fea-153">In the ![3][3] section of the blade, the ExpressRoute essentials are listed as shown in the following screen shot:</span></span>

<span data-ttu-id="07fea-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="07fea-154">![4][4]</span></span>    

<span data-ttu-id="07fea-155">Параметр *Состояние цепи* в разделе основных сведений об ExpressRoute указывает состояние канала на стороне Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="07fea-155">In the ExpressRoute Essentials, *Circuit status* indicates the status of the circuit on the Microsoft side.</span></span> <span data-ttu-id="07fea-156">Параметр *Состояние поставщика* указывает, был ли канал *подготовлен* на стороне поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="07fea-156">*Provider status* indicates if the circuit has been *Provisioned/Not provisioned* on the service-provider side.</span></span> 

<span data-ttu-id="07fea-157">Для работы канала ExpressRoute параметр *Состояние цепи* должен иметь значение *Включено*, а параметр *Состояние поставщика* — значение *Подготовлено*.</span><span class="sxs-lookup"><span data-stu-id="07fea-157">For an ExpressRoute circuit to be operational, the *Circuit status* must be *Enabled* and the *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="07fea-158">Если параметр *Состояние цепи* имеет значение "Не включено", обратитесь в [службу поддержки Майкрософт][Support].</span><span class="sxs-lookup"><span data-stu-id="07fea-158">If the *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="07fea-159">Если параметр *Состояние поставщика* имеет значение "Не подготовлено", обратитесь к поставщику услуг связи.</span><span class="sxs-lookup"><span data-stu-id="07fea-159">If the *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="07fea-160">Проверка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="07fea-160">Verification via PowerShell</span></span>
<span data-ttu-id="07fea-161">Чтобы получить список всех каналов ExpressRoute в группе ресурсов, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07fea-161">To list all the ExpressRoute circuits in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="07fea-162">Имя группы ресурсов можно получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="07fea-162">You can get your resource group name through the Azure portal.</span></span> <span data-ttu-id="07fea-163">Перейдите к предыдущему подразделу этого документа и обратите внимание, что имя группы ресурсов указано на снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="07fea-163">See the previous subsection of this document and note that the resource group name is listed in the example screen shot.</span></span>
>
>

<span data-ttu-id="07fea-164">Чтобы выбрать конкретный канал ExpressRoute в группе ресурсов, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07fea-164">To select a particular ExpressRoute circuit in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="07fea-165">Пример ответа:</span><span class="sxs-lookup"><span data-stu-id="07fea-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="07fea-166">Чтобы подтвердить работоспособность канала ExpressRoute, обратите особое внимание на следующие поля:</span><span class="sxs-lookup"><span data-stu-id="07fea-166">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="07fea-167">Если параметр *CircuitProvisioningState* имеет значение Not Enabled, обратитесь в [службу поддержки Майкрософт][Support].</span><span class="sxs-lookup"><span data-stu-id="07fea-167">If the *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="07fea-168">Если параметр *ServiceProviderProvisioningState* имеет значение Not Provisioned, обратитесь к поставщику услуг связи.</span><span class="sxs-lookup"><span data-stu-id="07fea-168">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="07fea-169">Проверка с помощью PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="07fea-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="07fea-170">Чтобы получить список всех каналов ExpressRoute в подписке, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07fea-170">To list all the ExpressRoute circuits under a subscription, use the following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="07fea-171">Чтобы выбрать конкретный канал ExpressRoute, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07fea-171">To select a particular ExpressRoute circuit, use the following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="07fea-172">Пример ответа:</span><span class="sxs-lookup"><span data-stu-id="07fea-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="07fea-173">Чтобы подтвердить работоспособность канала ExpressRoute, обратите особое внимание на следующие поля: ServiceProviderProvisioningState: Provisioned; Status: Enabled.</span><span class="sxs-lookup"><span data-stu-id="07fea-173">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="07fea-174">Если параметр *Status* имеет значение Not Enabled, обратитесь в [службу поддержки Майкрософт][Support].</span><span class="sxs-lookup"><span data-stu-id="07fea-174">If the *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="07fea-175">Если параметр *ServiceProviderProvisioningState* имеет значение Not Provisioned, обратитесь к поставщику услуг связи.</span><span class="sxs-lookup"><span data-stu-id="07fea-175">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="07fea-176">Проверка настройки пиринга</span><span class="sxs-lookup"><span data-stu-id="07fea-176">Validate Peering Configuration</span></span>
<span data-ttu-id="07fea-177">Когда поставщик услуг завершит подготовку канала, можно создать конфигурацию маршрутизации через канал ExpressRoute между маршрутизаторами MSEE-PR (4) и MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="07fea-177">After the service provider has completed the provisioning the ExpressRoute circuit, a routing configuration can be created over the ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="07fea-178">Каждый канал ExpressRoute может иметь включенными один, два или три контекста маршрутизации: частный пиринг Azure (трафик к частным виртуальным сетям в Azure), общедоступный пиринг Azure (трафик к общедоступным IP-адресам в Azure) и пиринг Майкрософт (трафик к Office 365 и Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="07fea-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic to private virtual networks in Azure), Azure public peering (traffic to public IP addresses in Azure), and Microsoft peering (traffic to Office 365 and Dynamics 365).</span></span> <span data-ttu-id="07fea-179">Дополнительные сведения о создании и изменении настроек маршрутизации см. в статье [Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="07fea-179">For more information on how to create and modify routing configuration, see the article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="07fea-180">Проверка на портале Azure</span><span class="sxs-lookup"><span data-stu-id="07fea-180">Verification via the Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="07fea-181">На портале Azure есть известная ошибка: если пиринговую связь ExpressRoute настроил поставщик услуг связи, она *не* отображается на портале.</span><span class="sxs-lookup"><span data-stu-id="07fea-181">There is a known bug in the Azure portal wherein ExpressRoute peerings are *NOT* shown in the portal if configured by the service provider.</span></span> <span data-ttu-id="07fea-182">Добавление пиринга ExpressRoute с помощью портала или PowerShell *перезаписывает параметры поставщика услуг связи*.</span><span class="sxs-lookup"><span data-stu-id="07fea-182">Adding ExpressRoute peerings via the portal or PowerShell *overwrites the service provider settings*.</span></span> <span data-ttu-id="07fea-183">При этом маршрутизация к каналу ExpressRoute прерывается. Для возобновления нормальной маршрутизации необходимо обратиться к поставщику услуг связи, чтобы восстановить параметры.</span><span class="sxs-lookup"><span data-stu-id="07fea-183">This action breaks the routing on the ExpressRoute circuit and requires the support of the service provider to restore the settings and reestablish normal routing.</span></span> <span data-ttu-id="07fea-184">Изменяйте сеансы пиринга ExpressRoute, только если известно, что поставщик услуг связи предлагает только услуги уровня 2.</span><span class="sxs-lookup"><span data-stu-id="07fea-184">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="07fea-185">Если поставщик услуг связи предлагает услуги уровня 3 и сеансы пиринга на портале пусты, можно использовать PowerShell для просмотра параметров настройки поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="07fea-185">If layer 3 is provided by the service provider and the peerings are blank in the portal, PowerShell can be used to see the service provider configured settings.</span></span>
>
>

<span data-ttu-id="07fea-186">На портале Azure можно просмотреть состояние канала ExpressRoute, выбрав ![2][2] в боковом меню слева, а затем выбрав канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="07fea-186">In the Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="07fea-187">Выберите канал ExpressRoute в разделе "Все ресурсы", после чего откроется колонка канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="07fea-187">Selecting an ExpressRoute circuit listed under "All resources" would open the ExpressRoute circuit blade.</span></span> <span data-ttu-id="07fea-188">В ![3][3] разделе колонки отображаются основные сведения об ExpressRoute, как показано на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="07fea-188">In the ![3][3] section of the blade, the ExpressRoute essentials would be listed as shown in the following screen shot:</span></span>

<span data-ttu-id="07fea-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="07fea-189">![5][5]</span></span>

<span data-ttu-id="07fea-190">Как отмечалось в предыдущем примере, контекст маршрутизации частного пиринга Azure включен, тогда как контекст маршрутизации общедоступного пиринга Azure и пиринга Майкрософт отключен.</span><span class="sxs-lookup"><span data-stu-id="07fea-190">In the preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="07fea-191">Если контекст пиринга включен, в списке также отобразятся первичные и вторичные подсети типа "точка — точка" (требуется для BGP).</span><span class="sxs-lookup"><span data-stu-id="07fea-191">A successfully enabled peering context would also have the primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="07fea-192">Подсети /30 используются для IP-адреса интерфейса маршрутизаторов MSEE и PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-192">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="07fea-193">Если пиринг не включен, проверьте, соответствуют ли назначенные первичные и вторичные подсети конфигурации маршрутизаторов PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-193">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on PE-MSEEs.</span></span> <span data-ttu-id="07fea-194">Если это не так, см. сведения об изменении настроек маршрутизаторов MSEE в статье [Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="07fea-194">If not, to change the configuration on MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="07fea-195">Проверка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="07fea-195">Verification via PowerShell</span></span>
<span data-ttu-id="07fea-196">Чтобы получить дополнительные сведения о конфигурации частного пиринга Azure, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="07fea-196">To get the Azure private peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="07fea-197">Пример ответа в случае успешной настройки частного пиринга:</span><span class="sxs-lookup"><span data-stu-id="07fea-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="07fea-198">Если контекст пиринга включен, в списке отобразятся первичные и вторичные префиксы адресов.</span><span class="sxs-lookup"><span data-stu-id="07fea-198">A successfully enabled peering context would have the primary and secondary address prefixes listed.</span></span> <span data-ttu-id="07fea-199">Подсети /30 используются для IP-адреса интерфейса маршрутизаторов MSEE и PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-199">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="07fea-200">Чтобы получить дополнительные сведения о настройке общедоступного пиринга Azure, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="07fea-200">To get the Azure public peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="07fea-201">Чтобы получить дополнительные сведения о настройке пиринга Майкрософт, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="07fea-201">To get the Microsoft peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="07fea-202">Если пиринг не настроен, отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="07fea-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="07fea-203">Пример ответа, если указанный пиринг (в этом примере общедоступный пиринг Azure) не настроен в канале.</span><span class="sxs-lookup"><span data-stu-id="07fea-203">A sample response, when the stated peering (Azure Public peering in this example) is not configured within the circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="07fea-204">Если пиринг не включен, проверьте, соответствуют ли назначенные первичные и вторичные подсети конфигурации связанных маршрутизаторов PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-204">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="07fea-205">Кроме того, проверьте, используются ли в маршрутизаторах MSEE правильные значения *VlandI*, *AzureASN*, *PeerASN* и соответствуют ли они тем, которые используются в связанных маршрутизаторах PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-205">Also check if the correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="07fea-206">Если вы выбрали хэширование MD5, общий ключ должен быть одинаковым для пары маршрутизаторов MSEE и PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-206">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="07fea-207">Дополнительные сведения об изменении настроек маршрутизаторов MSEE см. в статье [Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="07fea-207">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="07fea-208">Проверка с помощью PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="07fea-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="07fea-209">Чтобы получить дополнительные сведения о настройке частного пиринга Azure, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="07fea-209">To get the Azure private peering configuration details, use the following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="07fea-210">Пример ответа в случае успешной настройки частного пиринга:</span><span class="sxs-lookup"><span data-stu-id="07fea-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="07fea-211">Если контекст пиринга включен, в списке отобразятся первичные и вторичные подсети.</span><span class="sxs-lookup"><span data-stu-id="07fea-211">A successfully, enabled peering context would have the primary and secondary peer subnets listed.</span></span> <span data-ttu-id="07fea-212">Подсети /30 используются для IP-адреса интерфейса маршрутизаторов MSEE и PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-212">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="07fea-213">Чтобы получить дополнительные сведения о настройке общедоступного пиринга Azure, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="07fea-213">To get the Azure public peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="07fea-214">Чтобы получить дополнительные сведения о настройке пиринга Майкрософт, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="07fea-214">To get the Microsoft peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="07fea-215">Если сеансы пиринга уровня 3 заданы поставщиком услуг, параметры сеансов пиринга ExpressRoute, настроенные на портале или в PowerShell, перезапишут параметры поставщика услуг связи.</span><span class="sxs-lookup"><span data-stu-id="07fea-215">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span></span> <span data-ttu-id="07fea-216">Для сброса параметров пиринга со стороны поставщика потребуется помощь службы поддержки поставщика услуг связи.</span><span class="sxs-lookup"><span data-stu-id="07fea-216">Resetting the provider side peering settings requires the support of the service provider.</span></span> <span data-ttu-id="07fea-217">Изменяйте сеансы пиринга ExpressRoute, только если известно, что поставщик услуг связи предлагает только услуги уровня 2.</span><span class="sxs-lookup"><span data-stu-id="07fea-217">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="07fea-218">Если пиринг не включен, проверьте, соответствуют ли назначенные первичные и вторичные пиринговые подсети конфигурации связанных маршрутизаторов PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-218">If a peering is not enabled, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="07fea-219">Кроме того, проверьте, используются ли в маршрутизаторах MSEE правильные значения *VlandI*, *AzureASN*, *PeerASN* и соответствуют ли они тем, которые используются в связанных маршрутизаторах PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-219">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="07fea-220">Дополнительные сведения об изменении настроек маршрутизаторов MSEE см. в статье [Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="07fea-220">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-the-service-provider"></a><span data-ttu-id="07fea-221">Проверка ARP между корпорацией Майкрософт и поставщиком услуг связи</span><span class="sxs-lookup"><span data-stu-id="07fea-221">Validate ARP between Microsoft and the service provider</span></span>
<span data-ttu-id="07fea-222">В этом разделе используются классические команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="07fea-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="07fea-223">Если вы использовали команды PowerShell для Azure Resource Manager, убедитесь, что у вас есть доступ администратора или соадминистратора к подписке с помощью [классического портала Azure][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="07fea-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="07fea-224">Сведения об устранении неполадок с помощью команд Azure Resource Manager см. в документе [Получение таблиц ARP в модели развертывания с помощью Resource Manager][ARP].</span><span class="sxs-lookup"><span data-stu-id="07fea-224">For troubleshooting using Azure Resource Manager commands please refer to the [Getting ARP tables in the Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="07fea-225">Чтобы получить ARP, можно использовать команды PowerShell для Azure Resource Manager и портал Azure.</span><span class="sxs-lookup"><span data-stu-id="07fea-225">To get ARP, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="07fea-226">Если при использовании команд PowerShell для Azure Resource Manager возникают ошибки, должны работать классические команды PowerShell так же, как классические команды PowerShell работают с каналами ExpressRoute в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="07fea-226">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="07fea-227">Для получения таблицы ARP из основного маршрутизатора MSEE частного пиринга используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07fea-227">To get the ARP table from the primary MSEE router for the private peering, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="07fea-228">Пример ответа в случае успешного результата:</span><span class="sxs-lookup"><span data-stu-id="07fea-228">An example response for the command, in the successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="07fea-229">Аналогичным образом можно проверить таблицу ARP из MSEE по *основному*/*дополнительному* пути для *частного*/*публичного* пиринга или пиринга /*Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="07fea-229">Similarly, you can check the ARP table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="07fea-230">В следующем примере показан ответ команды, если пиринг не существует.</span><span class="sxs-lookup"><span data-stu-id="07fea-230">The following example shows the response of the command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="07fea-231">Если в таблице ARP нет IP-адресов интерфейсов, сопоставленных с MAC-адресами, ознакомьтесь со следующими сведениями.</span><span class="sxs-lookup"><span data-stu-id="07fea-231">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
>1. <span data-ttu-id="07fea-232">Если первый IP-адрес подсети /30 назначен для связи между маршрутизатором MSEE-PR и MSEE используется интерфейсом MSEE-PR,</span><span class="sxs-lookup"><span data-stu-id="07fea-232">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="07fea-233">Azure всегда использует второй IP-адрес для маршрутизаторов MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-233">Azure always uses the second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="07fea-234">Убедитесь, что клиентские (C-тег) и служебные теги (S-тег) виртуальной сети соответствуют паре MSEE-PR и MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-234">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-the-msee"></a><span data-ttu-id="07fea-235">Проверка BGP и маршрутов MSEE</span><span class="sxs-lookup"><span data-stu-id="07fea-235">Validate BGP and routes on the MSEE</span></span>
<span data-ttu-id="07fea-236">В этом разделе используются классические команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="07fea-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="07fea-237">Если вы использовали команды PowerShell для Azure Resource Manager, убедитесь, что у вас есть доступ администратора или соадминистратора к подписке с помощью [классического портала Azure][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="07fea-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="07fea-238">Чтобы получить сведения о BGP, можно использовать команды PowerShell для Azure Resource Manager и портала Azure.</span><span class="sxs-lookup"><span data-stu-id="07fea-238">To get BGP information, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="07fea-239">Если при использовании команд PowerShell для Azure Resource Manager возникают ошибки, должны работать классические команды PowerShell так же, как классические команды PowerShell работают с каналами ExpressRoute в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="07fea-239">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="07fea-240">Чтобы получить сводные сведения о таблице маршрутизации (соседа BGP) для определенного контекста маршрутизации, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07fea-240">To get the routing table (BGP neighbor) summary for a particular routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="07fea-241">Пример ответа:</span><span class="sxs-lookup"><span data-stu-id="07fea-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="07fea-242">Как показано в предыдущем примере, команда полезна для определения того, как давно установлен контекст маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="07fea-242">As shown in the preceding example, the command is useful to determine for how long the routing context has been established.</span></span> <span data-ttu-id="07fea-243">Она также показывает число префиксов маршрутов, объявленных пиринговым маршрутизатором.</span><span class="sxs-lookup"><span data-stu-id="07fea-243">It also indicates number of route prefixes advertised by the peering router.</span></span>

>[!NOTE]
><span data-ttu-id="07fea-244">Если состояние имеет значение Active (Активно) или Idle (Простаивает), проверьте, соответствуют ли назначенные первичные и вторичные подсети конфигурации связанных маршрутизаторов PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-244">If the state is in Active or Idle, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="07fea-245">Кроме того, проверьте, используются ли в маршрутизаторах MSEE правильные значения *VlandI*, *AzureASN*, *PeerASN* и соответствуют ли они тем, которые используются в связанных маршрутизаторах PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-245">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="07fea-246">Если вы выбрали хэширование MD5, общий ключ должен быть одинаковым для пары маршрутизаторов MSEE и PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="07fea-246">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="07fea-247">Дополнительные сведения об изменении настроек маршрутизаторов MSEE см. в статье [Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="07fea-247">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="07fea-248">Если определенные получатели недоступны через определенный пиринг, проверьте таблицу маршрутов для маршрутизаторов MSEE, принадлежащих определенному контексту пиринга.</span><span class="sxs-lookup"><span data-stu-id="07fea-248">If certain destinations are not reachable over a particular peering, check the route table of the MSEEs belonging to the particular peering context.</span></span> <span data-ttu-id="07fea-249">Если соответствующий префикс (может быть преобразованный через NAT IP-адрес) присутствует в таблице маршрутизации, то проверьте, разрешают ли трафик существующие на пути брандмауэры, группы безопасности сети и списки управления доступом.</span><span class="sxs-lookup"><span data-stu-id="07fea-249">If a matching prefix (could be NATed IP) is present in the routing table, then check if there are firewalls/NSG/ACLs on the path and if they permit the traffic.</span></span>
>
>

<span data-ttu-id="07fea-250">Чтобы получить полную таблицу маршрутизации из MSEE по *основному* пути для конкретного *частного* контекста маршрутизации, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07fea-250">To get the full routing table from MSEE on the *Primary* path for the particular *Private* routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="07fea-251">Пример ответа в случае успешного результата:</span><span class="sxs-lookup"><span data-stu-id="07fea-251">An example successful outcome for the command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="07fea-252">Аналогичным образом можно проверить таблицу маршрутизации из MSEE по *основному*/*дополнительному* пути для *частного*/*публичного* пиринга или пиринга/ *Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="07fea-252">Similarly, you can check the routing table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="07fea-253">В следующем примере показан ответ команды, если пиринг не существует.</span><span class="sxs-lookup"><span data-stu-id="07fea-253">The following example shows the response of the command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-the-traffic-statistics"></a><span data-ttu-id="07fea-254">Проверка статистики трафика</span><span class="sxs-lookup"><span data-stu-id="07fea-254">Check the Traffic Statistics</span></span>
<span data-ttu-id="07fea-255">Для получения сводной статистики трафика (переданных и полученных байтов) по первичному и вторичному пути для контекста пиринга используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07fea-255">To get the combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use the following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="07fea-256">Пример результата выполнения команды:</span><span class="sxs-lookup"><span data-stu-id="07fea-256">A sample output of the command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="07fea-257">Пример результата выполнения команды при отсутствующем пиринге:</span><span class="sxs-lookup"><span data-stu-id="07fea-257">A sample output of the command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="07fea-258">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07fea-258">Next Steps</span></span>
<span data-ttu-id="07fea-259">Дополнительные сведения доступны в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="07fea-259">For more information or help, check out the following links:</span></span>

- <span data-ttu-id="07fea-260">[Служба технической поддержки Майкрософт][Support]</span><span class="sxs-lookup"><span data-stu-id="07fea-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="07fea-261">[Создание и изменение канала ExpressRoute][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="07fea-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="07fea-262">[Создание и изменение маршрутизации для канала ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="07fea-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
<span data-ttu-id="07fea-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Логическое подключение ExpressRoute"</span><span class="sxs-lookup"><span data-stu-id="07fea-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity"</span></span>
<span data-ttu-id="07fea-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Значок "Все ресурсы""</span><span class="sxs-lookup"><span data-stu-id="07fea-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "All resources icon"</span></span>
<span data-ttu-id="07fea-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Значок "Обзор""</span><span class="sxs-lookup"><span data-stu-id="07fea-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overview icon"</span></span>
<span data-ttu-id="07fea-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Снимок экран раздела с основными сведениями об ExpressRoute"</span><span class="sxs-lookup"><span data-stu-id="07fea-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials sample screenshot"</span></span>
<span data-ttu-id="07fea-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Снимок экран раздела с основными сведениями об ExpressRoute"</span><span class="sxs-lookup"><span data-stu-id="07fea-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials sample screenshot"</span></span>

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






