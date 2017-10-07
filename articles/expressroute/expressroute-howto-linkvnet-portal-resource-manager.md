---
title: "Связывание виртуальной сети tooan канал ExpressRoute: портал Azure | Документы Microsoft"
description: "Этот документ содержит общие сведения о том, как toolink виртуальных сетей (Vnet) tooExpressRoute цепи."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="af797-103">Подключение виртуальной сети tooan канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="af797-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af797-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="af797-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="af797-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af797-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="af797-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="af797-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="af797-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="af797-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="af797-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="af797-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="af797-109">Эта статья поможет вам связать каналы ExpressRoute tooAzure виртуальных сетей (Vnet) с помощью модели развертывания диспетчера ресурсов hello и hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="af797-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and hello Azure portal.</span></span> <span data-ttu-id="af797-110">Виртуальные сети могут быть в hello той же подписке, или они могут быть частью другую подписку.</span><span class="sxs-lookup"><span data-stu-id="af797-110">Virtual networks can either be in hello same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="af797-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="af797-111">Before you begin</span></span>
* <span data-ttu-id="af797-112">Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="af797-112">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="af797-113">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af797-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="af797-114">Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и иметь цепи hello, предоставляемой поставщиком соединения.</span><span class="sxs-lookup"><span data-stu-id="af797-114">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="af797-115">Убедитесь, что для вашего канала настроен частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="af797-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="af797-116">В разделе hello [Настройка маршрутизации](expressroute-howto-routing-portal-resource-manager.md) маршрутизации инструкции.</span><span class="sxs-lookup"><span data-stu-id="af797-116">See hello [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="af797-117">Убедитесь, что настроен открытого пиринга Azure и hello пиринга BGP между вашей сетью и Майкрософт работает так, чтобы можно было включить подключение начала до конца.</span><span class="sxs-lookup"><span data-stu-id="af797-117">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="af797-118">Вам необходимо создать и полностью подготовить виртуальную сеть и шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="af797-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="af797-119">Следуйте инструкциям hello слишком[создать шлюз виртуальной сети для ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="af797-119">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="af797-120">Шлюз виртуальной сети для ExpressRoute использует hello «ExpressRoute», тип шлюза не VPN.</span><span class="sxs-lookup"><span data-stu-id="af797-120">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="af797-121">Объедините too10 виртуальных сетей tooa стандартные каналом expressroute.</span><span class="sxs-lookup"><span data-stu-id="af797-121">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="af797-122">Все виртуальные сети должны быть в hello геополитические совпадают при использовании стандартных канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af797-122">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="af797-123">Связывание виртуальной сети за пределами области геополитические hello объекта hello канал ExpressRoute или подключения большее количество виртуальных сетей tooyour канал ExpressRoute, если вы включили hello ExpressRoute премиальное дополнение.</span><span class="sxs-lookup"><span data-stu-id="af797-123">You can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="af797-124">Проверьте hello [часто задаваемые вопросы о](expressroute-faqs.md) Дополнительные сведения о премиальное дополнение hello.</span><span class="sxs-lookup"><span data-stu-id="af797-124">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>
* <span data-ttu-id="af797-125">Вы можете [просмотреть видео](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) до начала toobetter понять hello действия.</span><span class="sxs-lookup"><span data-stu-id="af797-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning toobetter understand hello steps.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="af797-126">Подключить виртуальную сеть в Привет одному каналу tooa подписки</span><span class="sxs-lookup"><span data-stu-id="af797-126">Connect a virtual network in hello same subscription tooa circuit</span></span>

### <a name="toocreate-a-connection"></a><span data-ttu-id="af797-127">toocreate соединение</span><span class="sxs-lookup"><span data-stu-id="af797-127">toocreate a connection</span></span>

> [!NOTE]
> <span data-ttu-id="af797-128">Сведения о конфигурации BGP не будет отображаться при hello уровня 3 поставщик настроен на пиринги.</span><span class="sxs-lookup"><span data-stu-id="af797-128">BGP configuration information will not show up if hello layer 3 provider configured your peerings.</span></span> <span data-ttu-id="af797-129">Если ваш канал находится в состоянии, подготовленных, должен быть toocreate возможности подключения.</span><span class="sxs-lookup"><span data-stu-id="af797-129">If your circuit is in a provisioned state, you should be able toocreate connections.</span></span>
>

1. <span data-ttu-id="af797-130">Убедитесь, что канал ExpressRoute и частный пиринг Azure настроены.</span><span class="sxs-lookup"><span data-stu-id="af797-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="af797-131">Следуйте инструкциям в разделе hello [создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и [Настройка маршрутизации](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="af797-131">Follow hello instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="af797-132">Ваш канал ExpressRoute должна выглядеть hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="af797-132">Your ExpressRoute circuit should look like hello following image:</span></span>

    ![Снимок экрана канала ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="af797-134">Теперь вы можете запустить подготовку toolink подключения вашей виртуальной сети шлюза tooyour канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af797-134">You can now start provisioning a connection toolink your virtual network gateway tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="af797-135">Нажмите кнопку **подключения** > **добавить** tooopen hello **добавить подключение** колонке и затем настройте значения hello.</span><span class="sxs-lookup"><span data-stu-id="af797-135">Click **Connection** > **Add** tooopen hello **Add connection** blade, and then configure hello values.</span></span>

    ![Снимок экрана добавления подключения](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="af797-137">После успешной настройки подключения к объект подключения будет показана информация hello hello подключения.</span><span class="sxs-lookup"><span data-stu-id="af797-137">After your connection has been successfully configured, your connection object will show hello information for hello connection.</span></span>

     ![Снимок экрана объекта подключения](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a><span data-ttu-id="af797-139">toodelete соединение</span><span class="sxs-lookup"><span data-stu-id="af797-139">toodelete a connection</span></span>
<span data-ttu-id="af797-140">Подключение можно удалить, выбрав hello **удалить** значок колонке hello для соединения.</span><span class="sxs-lookup"><span data-stu-id="af797-140">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="af797-141">Подключить виртуальную сеть в цепи tooa другой подписке</span><span class="sxs-lookup"><span data-stu-id="af797-141">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="af797-142">Канал ExpressRoute может совместно использоваться несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="af797-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="af797-143">на следующем рисунке Hello показана простая схема способ управления доступом подходит для каналов ExpressRoute в нескольких подписках.</span><span class="sxs-lookup"><span data-stu-id="af797-143">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Подключение между подписками](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="af797-145">Каждый из hello маленькие облака в облако hello является используется toorepresent подписках, которые принадлежат toodifferent отделам в организации.</span><span class="sxs-lookup"><span data-stu-id="af797-145">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span>
- <span data-ttu-id="af797-146">Каждый из отделов hello hello организации можно использовать собственную подписку для развертывания своих служб, но они могут совместно использовать одной ExpressRoute цепи tooconnect tooyour назад в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="af797-146">Each of hello departments within hello organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span>
- <span data-ttu-id="af797-147">Одному отделу (в этом примере: ИТ) может быть владельцем hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af797-147">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="af797-148">Другие подписки в hello организации можно использовать канал ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="af797-148">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af797-149">Плата за подключение и пропускную способность для hello выделенного канала будет применен toohello владельца канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af797-149">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="af797-150">Все виртуальные сети совместно использовать hello же пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="af797-150">All virtual networks share hello same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="af797-151">Администрирование: владельцы канала и его пользователи</span><span class="sxs-lookup"><span data-stu-id="af797-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="af797-152">Hello «владелец схемы» зарегистрирован как авторизованный пользователь питания, для hello ресурсов цепь ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af797-152">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="af797-153">Владелец канала Hello можно создать авторизацию, может быть активирован с «канала пользователи».</span><span class="sxs-lookup"><span data-stu-id="af797-153">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="af797-154">Пользователи канала являются владельцами виртуальной сети hello шлюзов, которые не находятся в одной подписке, как hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af797-154">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="af797-155">Пользователи канала могут активировать разрешения (по одному разрешению для каждой виртуальной сети).</span><span class="sxs-lookup"><span data-stu-id="af797-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="af797-156">Владелец канала Hello имеет авторизаций toomodify и revoke power hello в любое время.</span><span class="sxs-lookup"><span data-stu-id="af797-156">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="af797-157">Отмена авторизации приведет все подключения ссылку, удаляемый из подписки hello, доступ к которым был отозван.</span><span class="sxs-lookup"><span data-stu-id="af797-157">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="af797-158">Действия владельца канала</span><span class="sxs-lookup"><span data-stu-id="af797-158">Circuit owner operations</span></span>

<span data-ttu-id="af797-159">**toocreate авторизации подключения**</span><span class="sxs-lookup"><span data-stu-id="af797-159">**toocreate a connection authorization**</span></span>

<span data-ttu-id="af797-160">Владелец канала Hello создает авторизации.</span><span class="sxs-lookup"><span data-stu-id="af797-160">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="af797-161">Это приведет к создание hello ключ авторизации, которое может быть используемые схемы пользователя tooconnect их toohello шлюзы виртуальной сети канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af797-161">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="af797-162">Разрешение действительно только для одного подключения.</span><span class="sxs-lookup"><span data-stu-id="af797-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="af797-163">В колонке hello ExpressRoute выберите **авторизаций** , а затем введите **имя** для авторизации hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="af797-163">In hello ExpressRoute blade, Click **Authorizations** and then type a **name** for hello authorization and click **Save**.</span></span>

    ![Authorizations](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="af797-165">После сохранения конфигурации hello скопируйте hello **идентификатор ресурса** и hello **ключ авторизации**.</span><span class="sxs-lookup"><span data-stu-id="af797-165">Once hello configuration is saved, copy hello **Resource ID** and hello **Authorization Key**.</span></span>

    ![Ключ авторизации](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="af797-167">**toodelete авторизации подключения**</span><span class="sxs-lookup"><span data-stu-id="af797-167">**toodelete a connection authorization**</span></span>

<span data-ttu-id="af797-168">Подключение можно удалить, выбрав hello **удалить** значок колонке hello для соединения.</span><span class="sxs-lookup"><span data-stu-id="af797-168">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="af797-169">Действия пользователя канала</span><span class="sxs-lookup"><span data-stu-id="af797-169">Circuit user operations</span></span>

<span data-ttu-id="af797-170">Hello канала пользователю требуется идентификатор ресурса hello и ключ авторизации от владельца канала hello.</span><span class="sxs-lookup"><span data-stu-id="af797-170">hello circuit user needs hello resource ID and an authorization key from hello circuit owner.</span></span> 

<span data-ttu-id="af797-171">**tooredeem авторизации подключения**</span><span class="sxs-lookup"><span data-stu-id="af797-171">**tooredeem a connection authorization**</span></span>

1.  <span data-ttu-id="af797-172">Нажмите кнопку hello **+ создать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="af797-172">Click hello **+New** button.</span></span>

    ![Нажмите кнопку "Создать"](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="af797-174">Поиск **«Соединения»** в hello Marketplace, выберите его и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="af797-174">Search for **"Connection"** in hello Marketplace, select it, and click **Create**.</span></span>

    ![Поиск подключений](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="af797-176">Убедитесь, что hello **тип подключения** задано слишком «ExpressRoute».</span><span class="sxs-lookup"><span data-stu-id="af797-176">Make sure hello **Connection type** is set too"ExpressRoute".</span></span>


4.  <span data-ttu-id="af797-177">Введите сведения о hello, а затем нажмите кнопку **ОК** в колонке основы hello.</span><span class="sxs-lookup"><span data-stu-id="af797-177">Fill in hello details, then click **OK** in hello Basics blade.</span></span>

    ![Колонка «Основные»](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="af797-179">В hello **параметры** колонки, выберите hello **шлюз виртуальной сети** и проверьте hello **активировать авторизации** флажок.</span><span class="sxs-lookup"><span data-stu-id="af797-179">In hello **Settings** blade, Select hello **Virtual network gateway** and check hello **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="af797-180">Введите hello **ключ авторизации** и hello **однорангового узла схемы URI** и присвойте имя подключения hello.</span><span class="sxs-lookup"><span data-stu-id="af797-180">Enter hello **Authorization key** and hello **Peer circuit URI** and give hello connection a name.</span></span> <span data-ttu-id="af797-181">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="af797-181">Click **OK**.</span></span>

    ![Колонка "Настройки"](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="af797-183">Просмотрите сведения о hello в hello **Сводка** колонку и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="af797-183">Review hello information in hello **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="af797-184">**toorelease авторизации подключения**</span><span class="sxs-lookup"><span data-stu-id="af797-184">**toorelease a connection authorization**</span></span>

<span data-ttu-id="af797-185">Авторизации можно освободить путем удаления соединений hello, связывающий hello цепь ExpressRoute toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="af797-185">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af797-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af797-186">Next steps</span></span>
<span data-ttu-id="af797-187">Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="af797-187">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
