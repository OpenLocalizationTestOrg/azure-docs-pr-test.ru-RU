---
title: "Связывание виртуальной сети с каналом ExpressRoute с помощью портала Azure | Документация Майкрософт"
description: "В этой статье кратко описывается процедура связывания виртуальных сетей с каналами ExpressRoute."
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
ms.openlocfilehash: 595c30ab5d9adc6061ad753d952adf894ba80b2f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="a42fd-103">Подключение виртуальной сети к каналу ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a42fd-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a42fd-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="a42fd-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="a42fd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a42fd-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="a42fd-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="a42fd-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="a42fd-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="a42fd-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="a42fd-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="a42fd-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="a42fd-109">В этой статье содержатся сведения о связывании виртуальных сетей с каналами Azure ExpressRoute с помощью модели развертывания Resource Manager и портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a42fd-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and the Azure portal.</span></span> <span data-ttu-id="a42fd-110">Виртуальные сети могут быть в той же или другой подписке.</span><span class="sxs-lookup"><span data-stu-id="a42fd-110">Virtual networks can either be in the same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a42fd-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a42fd-111">Before you begin</span></span>
* <span data-ttu-id="a42fd-112">Прежде чем приступить к настройке, изучите [предварительные требования](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md) и [рабочие процессы](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="a42fd-112">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="a42fd-113">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a42fd-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="a42fd-114">Следуйте инструкциям, чтобы [создать канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и включить его на стороне поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="a42fd-114">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="a42fd-115">Убедитесь, что для вашего канала настроен частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="a42fd-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="a42fd-116">Инструкции по маршрутизации см. в статье [Настройка маршрутизации](expressroute-howto-routing-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a42fd-116">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="a42fd-117">Для создания сквозного подключения обязательно настройте частный пиринг Azure, а также пиринг BGP между вашей сетью и сетью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="a42fd-117">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="a42fd-118">Вам необходимо создать и полностью подготовить виртуальную сеть и шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a42fd-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="a42fd-119">Следуйте инструкциям по [созданию шлюза виртуальной сети для ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a42fd-119">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="a42fd-120">Для ExpressRoute используется шлюз виртуальной сети типа ExpressRoute, а не VPN.</span><span class="sxs-lookup"><span data-stu-id="a42fd-120">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="a42fd-121">К стандартному каналу ExpressRoute можно подключить не более 10 виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="a42fd-121">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="a42fd-122">Если используется стандартный канал ExpressRoute, все виртуальные сети должны находиться в одном геополитическом регионе.</span><span class="sxs-lookup"><span data-stu-id="a42fd-122">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="a42fd-123">Если включить надстройку ExpressRoute Premium, вы сможете подключить к каналу ExpressRoute больше виртуальных сетей, включая сети из других геополитических регионов.</span><span class="sxs-lookup"><span data-stu-id="a42fd-123">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="a42fd-124">Дополнительную информацию о надстройке Premium см. в разделе [Вопросы и ответы](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a42fd-124">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>
* <span data-ttu-id="a42fd-125">Вы можете [просмотреть видео](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit), прежде чем начать, чтобы лучше понять выполняемые действия.</span><span class="sxs-lookup"><span data-stu-id="a42fd-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="a42fd-126">Подключение к каналу виртуальной сети в той же подписке</span><span class="sxs-lookup"><span data-stu-id="a42fd-126">Connect a virtual network in the same subscription to a circuit</span></span>

### <a name="to-create-a-connection"></a><span data-ttu-id="a42fd-127">Создание подключения</span><span class="sxs-lookup"><span data-stu-id="a42fd-127">To create a connection</span></span>

> [!NOTE]
> <span data-ttu-id="a42fd-128">Если пиринги были настроены поставщиком уровня 3, сведения о конфигурации BGP отображаться не будут.</span><span class="sxs-lookup"><span data-stu-id="a42fd-128">BGP configuration information will not show up if the layer 3 provider configured your peerings.</span></span> <span data-ttu-id="a42fd-129">Если канал находится в подготовленном состоянии, то вы сможете создавать подключения.</span><span class="sxs-lookup"><span data-stu-id="a42fd-129">If your circuit is in a provisioned state, you should be able to create connections.</span></span>
>

1. <span data-ttu-id="a42fd-130">Убедитесь, что канал ExpressRoute и частный пиринг Azure настроены.</span><span class="sxs-lookup"><span data-stu-id="a42fd-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="a42fd-131">Следуйте инструкциям в разделах [Создание и изменение канала ExpressRoute](expressroute-howto-circuit-arm.md) и [Создание и изменение маршрутизации для канала ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a42fd-131">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="a42fd-132">Ваш канал ExpressRoute должен выглядеть, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="a42fd-132">Your ExpressRoute circuit should look like the following image:</span></span>

    ![Снимок экрана канала ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="a42fd-134">Теперь можно приступить к подготовке подключения для связи шлюза виртуальной сети с каналом ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a42fd-134">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span></span> <span data-ttu-id="a42fd-135">Щелкните **Подключение** > **Добавить**, чтобы открыть колонку **Добавление подключения**, и укажите необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="a42fd-135">Click **Connection** > **Add** to open the **Add connection** blade, and then configure the values.</span></span>

    ![Снимок экрана добавления подключения](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="a42fd-137">После успешной настройки подключения в вашем объекте подключения будут показаны сведения о подключении.</span><span class="sxs-lookup"><span data-stu-id="a42fd-137">After your connection has been successfully configured, your connection object will show the information for the connection.</span></span>

     ![Снимок экрана объекта подключения](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="to-delete-a-connection"></a><span data-ttu-id="a42fd-139">Удаление подключения</span><span class="sxs-lookup"><span data-stu-id="a42fd-139">To delete a connection</span></span>
<span data-ttu-id="a42fd-140">Подключение можно удалить, щелкнув значок **Удалить** в колонке для подключения.</span><span class="sxs-lookup"><span data-stu-id="a42fd-140">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="a42fd-141">Подключение к каналу виртуальной сети в другой подписке</span><span class="sxs-lookup"><span data-stu-id="a42fd-141">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="a42fd-142">Канал ExpressRoute может совместно использоваться несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="a42fd-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="a42fd-143">На рисунке ниже схематично показан способ совместного использования каналов ExpressRoute несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="a42fd-143">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Подключение между подписками](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="a42fd-145">Каждое маленькое облако внутри большого облака представляет подписки, принадлежащие различным подразделениям одной организации.</span><span class="sxs-lookup"><span data-stu-id="a42fd-145">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span>
- <span data-ttu-id="a42fd-146">Любое подразделение в организации может использовать свою собственную подписку для развертывания служб. Кроме того, оно может совместно использовать один выделенный канал ExpressRoute для подключения к корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="a42fd-146">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span>
- <span data-ttu-id="a42fd-147">Владельцем канала ExpressRoute может выступать одно подразделение (в данном примере — ИТ-подразделение).</span><span class="sxs-lookup"><span data-stu-id="a42fd-147">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="a42fd-148">Другие подписки в организации могут использовать канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a42fd-148">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a42fd-149">Плата за подключение выделенного канала ExpressRoute и использование полосы пропускания будет взиматься с владельца выделенного канала.</span><span class="sxs-lookup"><span data-stu-id="a42fd-149">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="a42fd-150">Полоса пропускания распределяется между всеми виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="a42fd-150">All virtual networks share the same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="a42fd-151">Администрирование: владельцы канала и его пользователи</span><span class="sxs-lookup"><span data-stu-id="a42fd-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="a42fd-152">Владельцем канала является уполномоченный опытный пользователь ресурса канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a42fd-152">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="a42fd-153">Владелец канала может создавать разрешения, которые могут быть активированы пользователями канала.</span><span class="sxs-lookup"><span data-stu-id="a42fd-153">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="a42fd-154">Пользователи канала являются владельцами шлюзов виртуальных сетей (которые находятся в разных подписках с каналом ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="a42fd-154">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="a42fd-155">Пользователи канала могут активировать разрешения (по одному разрешению для каждой виртуальной сети).</span><span class="sxs-lookup"><span data-stu-id="a42fd-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="a42fd-156">Владелец канала имеет право изменить или отменить авторизацию в любое время.</span><span class="sxs-lookup"><span data-stu-id="a42fd-156">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="a42fd-157">Отмена разрешения приводит к удалению всех связывающих подключений из подписки, доступ к которой был отменен.</span><span class="sxs-lookup"><span data-stu-id="a42fd-157">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="a42fd-158">Действия владельца канала</span><span class="sxs-lookup"><span data-stu-id="a42fd-158">Circuit owner operations</span></span>

<span data-ttu-id="a42fd-159">**Создание разрешения на подключение**</span><span class="sxs-lookup"><span data-stu-id="a42fd-159">**To create a connection authorization**</span></span>

<span data-ttu-id="a42fd-160">Владелец канала создает разрешение.</span><span class="sxs-lookup"><span data-stu-id="a42fd-160">The circuit owner creates an authorization.</span></span> <span data-ttu-id="a42fd-161">Это приводит к созданию ключа разрешения, который может использоваться пользователем канала для подключения шлюзов виртуальной сети к каналу ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a42fd-161">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="a42fd-162">Разрешение действительно только для одного подключения.</span><span class="sxs-lookup"><span data-stu-id="a42fd-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="a42fd-163">В колонке "ExpressRoute" щелкните **Разрешения**, а затем введите **имя** авторизации и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a42fd-163">In the ExpressRoute blade, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span></span>

    ![Authorizations](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="a42fd-165">После сохранения конфигурации скопируйте **идентификатор ресурса** и **ключ авторизации**.</span><span class="sxs-lookup"><span data-stu-id="a42fd-165">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span></span>

    ![Ключ авторизации](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="a42fd-167">**Удаление разрешения на подключение**</span><span class="sxs-lookup"><span data-stu-id="a42fd-167">**To delete a connection authorization**</span></span>

<span data-ttu-id="a42fd-168">Подключение можно удалить, щелкнув значок **Удалить** в колонке для подключения.</span><span class="sxs-lookup"><span data-stu-id="a42fd-168">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="a42fd-169">Действия пользователя канала</span><span class="sxs-lookup"><span data-stu-id="a42fd-169">Circuit user operations</span></span>

<span data-ttu-id="a42fd-170">Пользователь канала должен получить от владельца канала идентификатор ресурса и ключ авторизации.</span><span class="sxs-lookup"><span data-stu-id="a42fd-170">The circuit user needs the resource ID and an authorization key from the circuit owner.</span></span> 

<span data-ttu-id="a42fd-171">**Активация разрешения на подключение**</span><span class="sxs-lookup"><span data-stu-id="a42fd-171">**To redeem a connection authorization**</span></span>

1.  <span data-ttu-id="a42fd-172">Нажмите кнопку **+Создать**.</span><span class="sxs-lookup"><span data-stu-id="a42fd-172">Click the **+New** button.</span></span>

    ![Нажмите кнопку "Создать"](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="a42fd-174">Найдите элемент **Подключение** на сайте Marketplace, выберите его и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a42fd-174">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span></span>

    ![Поиск подключений](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="a42fd-176">Убедитесь, что выбран **тип подключения** ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a42fd-176">Make sure the **Connection type** is set to "ExpressRoute".</span></span>


4.  <span data-ttu-id="a42fd-177">Введите необходимые сведения и нажмите кнопку **ОК** в колонке "Основные".</span><span class="sxs-lookup"><span data-stu-id="a42fd-177">Fill in the details, then click **OK** in the Basics blade.</span></span>

    ![Колонка «Основные»](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="a42fd-179">В колонке **Параметры** выберите **Шлюз виртуальной сети** и установите флажок **Redeem authorization** (Активировать авторизацию).</span><span class="sxs-lookup"><span data-stu-id="a42fd-179">In the **Settings** blade, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="a42fd-180">Введите значения **Ключ авторизации** и **Peer circuit URI** (URI однорангового канала) и присвойте подключению имя.</span><span class="sxs-lookup"><span data-stu-id="a42fd-180">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span></span> <span data-ttu-id="a42fd-181">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a42fd-181">Click **OK**.</span></span>

    ![Колонка "Настройки"](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="a42fd-183">Просмотрите сведения в колонке **Сводка** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a42fd-183">Review the information in the **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="a42fd-184">**Освобождение разрешения на подключение**</span><span class="sxs-lookup"><span data-stu-id="a42fd-184">**To release a connection authorization**</span></span>

<span data-ttu-id="a42fd-185">Разрешение можно освободить, удалив подключение, связывающее канал ExpressRoute и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="a42fd-185">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a42fd-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a42fd-186">Next steps</span></span>
<span data-ttu-id="a42fd-187">Дополнительные сведения об ExpressRoute см. в статье [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a42fd-187">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
