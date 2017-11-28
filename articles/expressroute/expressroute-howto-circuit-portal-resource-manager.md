---
title: "Создание и изменение канала ExpressRoute с помощью портала Azure | Документация Майкрософт"
description: "В этой статье описывается, как toocreate, подготовки, проверьте, обновление, удаление и отзыв канал ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="8ca2b-103">Создание и изменение канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ca2b-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ca2b-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="8ca2b-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="8ca2b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ca2b-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="8ca2b-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8ca2b-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="8ca2b-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="8ca2b-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="8ca2b-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="8ca2b-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="8ca2b-109">В этой статье описывается, как toocreate канал Azure ExpressRoute с помощью hello Azure hello и портал Azure модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-109">This article describes how toocreate an Azure ExpressRoute circuit by using hello Azure portal and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="8ca2b-110">Hello следующие шаги также показано, как toocheck hello состояние канала hello, обновления или удаления и сделать.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-110">hello following steps also show you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="8ca2b-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="8ca2b-111">Before you begin</span></span>
* <span data-ttu-id="8ca2b-112">Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-112">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="8ca2b-113">Убедитесь, что доступ toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ca2b-113">Ensure that you have access toohello [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="8ca2b-114">Убедитесь, что имеются разрешения toocreate новых сетевых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-114">Ensure that you have permissions toocreate new networking resources.</span></span> <span data-ttu-id="8ca2b-115">Обратитесь к администратору учетной записи, если нет соответствующих разрешений hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-115">Contact your account administrator if you do not have hello right permissions.</span></span>
* <span data-ttu-id="8ca2b-116">Вы можете [просмотреть видео](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) перед началом в порядке toobetter понять hello действия.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order toobetter understand hello steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="8ca2b-117">Создание и предоставление канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ca2b-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-toohello-azure-portal"></a><span data-ttu-id="8ca2b-118">1. Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8ca2b-118">1. Sign in toohello Azure portal</span></span>
<span data-ttu-id="8ca2b-119">В браузере перейдите toohello [портал Azure](http://portal.azure.com) и выполните вход с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-119">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="8ca2b-120">2. Создание канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ca2b-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8ca2b-121">Ваш канал ExpressRoute будет записана с момента hello выдачи ключа службы.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-121">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="8ca2b-122">Убедитесь, что эта операция при готовности tooprovision hello цепи hello поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-122">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

1. <span data-ttu-id="8ca2b-123">Можно создать канал ExpressRoute, выбрав параметр toocreate hello новый ресурс.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-123">You can create an ExpressRoute circuit by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="8ca2b-124">Нажмите кнопку **New** > **сети** > **ExpressRoute**, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="8ca2b-124">Click **New** > **Networking** > **ExpressRoute**, as shown in hello following image:</span></span>
   
    ![Создание канала ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="8ca2b-126">После нажатия кнопки **ExpressRoute**, вы увидите hello **канал ExpressRoute создания** колонку.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-126">After you click **ExpressRoute**, you'll see hello **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="8ca2b-127">Если вы заполнение значений hello в этой колонке, убедитесь, что указан правильный уровень номера SKU hello и измерение данных.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-127">When you're filling in hello values on this blade, make sure that you specify hello correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="8ca2b-128">**Уровень** определяет, какого уровня надстройка включена — ExpressRoute "Стандартный" или ExpressRoute "Премиум".</span><span class="sxs-lookup"><span data-stu-id="8ca2b-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="8ca2b-129">Можно указать **Стандартная** tooget hello стандартном номере SKU или **Premium** hello premium надстройки.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-129">You can specify **Standard** tooget hello standard SKU or **Premium** for hello premium add-on.</span></span>
   * <span data-ttu-id="8ca2b-130">**Измерение данных** определяет hello выставления счетов с типом.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-130">**Data metering** determines hello billing type.</span></span> <span data-ttu-id="8ca2b-131">Выберите **С учетом трафика** для тарифного плана с оплатой за трафик или **Не ограничено** для безлимитного тарифного плана.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="8ca2b-132">Обратите внимание, что можно изменить hello выставления счетов с типом из **Metered** слишком**неограниченное количество**, но не может изменить тип hello из **неограниченное количество** слишком**Metered**.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-132">Note that you can change hello billing type from **Metered** too**Unlimited**, but you can't change hello type from **Unlimited** too**Metered**.</span></span>
     
     ![Настройте уровень номера SKU hello и измерение данных](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="8ca2b-134">Имейте в виду, что расположение Пиринга hello указывает hello [физическое расположение](expressroute-locations.md) где вы пиринг с корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-134">Please be aware that hello Peering Location indicates hello [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="8ca2b-135">Это **не** слишком связанные свойства «Местоположение», которое ссылается toohello geography, где находится hello поставщика сетевых ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-135">This is **not** linked too"Location" property, which refers toohello geography where hello Azure Network Resource Provider is located.</span></span> <span data-ttu-id="8ca2b-136">Они не связаны, но это хорошей практикой toochoose расположение Пиринга канала hello территориально закрыть toohello поставщика сетевых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-136">While they are not related, it is a good practice toochoose a Network Resource Provider geographically close toohello Peering Location of hello circuit.</span></span> 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a><span data-ttu-id="8ca2b-137">3. Представление hello цепи и свойства</span><span class="sxs-lookup"><span data-stu-id="8ca2b-137">3. View hello circuits and properties</span></span>
<span data-ttu-id="8ca2b-138">**Просмотреть все каналы hello**</span><span class="sxs-lookup"><span data-stu-id="8ca2b-138">**View all hello circuits**</span></span>

<span data-ttu-id="8ca2b-139">Можно просмотреть все каналы hello, созданной при выборе **все ресурсы** hello меню слева.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-139">You can view all hello circuits that you created by selecting **All resources** on hello left-side menu.</span></span>

![Просмотр каналов](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="8ca2b-141">**Просмотр свойств hello**</span><span class="sxs-lookup"><span data-stu-id="8ca2b-141">**View hello properties**</span></span>

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Свойства](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="8ca2b-143">4. Отправка ключа tooyour подключения hello службы поставщика для подготовки</span><span class="sxs-lookup"><span data-stu-id="8ca2b-143">4. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="8ca2b-144">В этой колонке **состояние поставщика** предоставляет сведения о hello текущее состояние подготовки на стороне поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-144">On this blade, **Provider status** provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="8ca2b-145">**Circuit состояние** предоставляет hello состояния на стороне Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-145">**Circuit status** provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="8ca2b-146">Дополнительные сведения о состояния подготовки схемы см. в разделе hello [рабочих процессов](expressroute-workflows.md#expressroute-circuit-provisioning-states) статьи.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-146">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="8ca2b-147">При создании нового канала ExpressRoute hello схемы будут иметь hello следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="8ca2b-147">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

<span data-ttu-id="8ca2b-148">Состояние поставщика: Не подготовлено</span><span class="sxs-lookup"><span data-stu-id="8ca2b-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="8ca2b-149">Состояние канала: Включен</span><span class="sxs-lookup"><span data-stu-id="8ca2b-149">Circuit status: Enabled</span></span>

![Инициация процесса подготовки](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="8ca2b-151">цепь Hello приведет к изменению toohello при поставщика услуг подключения hello находится в процессе hello включить его для вас следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="8ca2b-151">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

<span data-ttu-id="8ca2b-152">Состояние поставщика: Идет подготовка</span><span class="sxs-lookup"><span data-stu-id="8ca2b-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="8ca2b-153">Состояние канала: Включен</span><span class="sxs-lookup"><span data-stu-id="8ca2b-153">Circuit status: Enabled</span></span>

<span data-ttu-id="8ca2b-154">Для вас toobe может toouse канал ExpressRoute он должен быть в hello следующие состояния:</span><span class="sxs-lookup"><span data-stu-id="8ca2b-154">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

<span data-ttu-id="8ca2b-155">Состояние поставщика: Подготовлено</span><span class="sxs-lookup"><span data-stu-id="8ca2b-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="8ca2b-156">Состояние канала: Включен</span><span class="sxs-lookup"><span data-stu-id="8ca2b-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="8ca2b-157">5. Периодически Проверьте состояние hello и состояние hello ключа канала hello</span><span class="sxs-lookup"><span data-stu-id="8ca2b-157">5. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="8ca2b-158">Можно просмотреть свойства hello hello канала, который вы хотите, выбрав его.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-158">You can view hello properties of hello circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="8ca2b-159">Проверьте hello **состояние поставщика** и убедитесь, что его следует переместить слишком**инициализировано** перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-159">Check hello **Provider status** and ensure that it has moved too**Provisioned** before you continue.</span></span>

![Состояние канала и поставщика](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="8ca2b-161">6. Создание конфигурации маршрутизации</span><span class="sxs-lookup"><span data-stu-id="8ca2b-161">6. Create your routing configuration</span></span>
<span data-ttu-id="8ca2b-162">Пошаговые инструкции см. в разделе toohello [expressroute в конфигурацию маршрутизации](expressroute-howto-routing-portal-resource-manager.md) статью toocreate и изменения пиринги в цепи.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-162">For step-by-step instructions, refer toohello [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ca2b-163">Эти инструкции применяются только toocircuits, созданных с помощью службы поставщиков, предлагающих услуги подключений второго уровня.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-163">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="8ca2b-164">Если вы работаете с поставщиком, предлагающим услуги третьего уровня (обычно это IPVPN, например MPLS), то ваш поставщик услуг подключения выполнит настройку и управление конфигурацией самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="8ca2b-165">7. Связывание виртуальной сети tooan канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ca2b-165">7. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="8ca2b-166">Затем свяжите виртуальной сети tooyour канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-166">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="8ca2b-167">Используйте hello [связывание виртуальной сети цепи tooExpressRoute](expressroute-howto-linkvnet-arm.md) статьи при работе с моделью развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-167">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="8ca2b-168">Получение состояния hello канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ca2b-168">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="8ca2b-169">Hello состояние канала можно просмотреть, выбрав его.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-169">You can view hello status of a circuit by selecting it.</span></span> 

![Состояние канала ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="8ca2b-171">Изменение канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ca2b-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="8ca2b-172">Некоторые свойства канала ExpressRoute можно изменить, не повлияв на подключение.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="8ca2b-173">Можно сделать hello без простоев следующие:</span><span class="sxs-lookup"><span data-stu-id="8ca2b-173">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="8ca2b-174">включать и отключать надстройку ExpressRoute "Премиум" для канала ExpressRoute;</span><span class="sxs-lookup"><span data-stu-id="8ca2b-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="8ca2b-175">Увеличение hello пропускной способностью вашего канала ExpressRoute при условии, что доступно емкости на порту hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-175">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="8ca2b-176">Обратите внимание, что понижение уровня полосы пропускания канала hello не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-176">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="8ca2b-177">Изменение плана на основе данных, измеряемые tooUnlimited данных отслеживания использования hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-177">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="8ca2b-178">Обратите внимание, изменяющихся план контроля использования программных продуктов hello из данных tooMetered данных не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-178">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="8ca2b-179">Параметр *Allow Classic Operations*(Разрешить классические операции) можно включать и отключать.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="8ca2b-180">Дополнительные сведения об ограничениях и ограничениях см. в разделе toohello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="8ca2b-180">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="8ca2b-181">Щелкните hello toomodify канал ExpressRoute **конфигурации** как показано на следующем рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-181">toomodify an ExpressRoute circuit, click on hello **Configuration** as shown in hello figure below.</span></span>

![Изменение канала](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="8ca2b-183">Можно изменить hello пропускной способности, SKU модели выставления счетов и разрешить классический операции в колонке конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-183">You can modify hello bandwidth, SKU, billing model and allow classic operations within hello configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ca2b-184">Канал ExpressRoute toorecreate hello возможно, если имеется существующий порт hello недостаточной мощности.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-184">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="8ca2b-185">Обновление схемы hello невозможно, если доступна без дополнительной емкости в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-185">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="8ca2b-186">Нельзя уменьшить hello пропускной способности канала ExpressRoute без прерывания.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-186">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="8ca2b-187">Понижение уровня полосы пропускания необходимо канал ExpressRoute toodeprovision hello и повторной инициализации новый канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-187">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="8ca2b-188">Отключить надстройку premium операция может завершиться неудачно, если вы используете ресурсы, которые больше, чем то, что разрешено для стандартной схемы hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="8ca2b-189">Отзыв и удаление канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ca2b-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="8ca2b-190">Ваш канал ExpressRoute можно удалить, выбрав hello **удалить** значок.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-190">You can delete your ExpressRoute circuit by selecting hello **delete** icon.</span></span> <span data-ttu-id="8ca2b-191">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="8ca2b-191">Note hello following:</span></span>

* <span data-ttu-id="8ca2b-192">Необходимо удалить связь всех виртуальных сетей с каналом expressroute hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-192">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="8ca2b-193">Если операция завершается неудачно, проверьте, связаны ли виртуальную сеть toohello канала.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-193">If this operation fails, check whether any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="8ca2b-194">Если состояние подготовки службы поставщика hello ExpressRoute канала **Provisioning** или **инициализировано** необходимо работать с ваш канал hello toodeprovision поставщика службы с их стороны.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-194">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="8ca2b-195">Она будет продолжать tooreserve ресурсы и выставлять вам счет на поставщика услуг hello завершения списания цепи hello и уведомляет нас.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-195">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="8ca2b-196">Если поставщик услуг hello отозваны hello канала (состояние подготовки поставщика услуг hello задано слишком**не инициализировано**) можно удалить цепь hello.</span><span class="sxs-lookup"><span data-stu-id="8ca2b-196">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="8ca2b-197">Это приведет к остановке выставления счетов для схемы hello</span><span class="sxs-lookup"><span data-stu-id="8ca2b-197">This will stop billing for hello circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ca2b-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8ca2b-198">Next steps</span></span>
<span data-ttu-id="8ca2b-199">После создания ваш канал, убедитесь, что hello следующие:</span><span class="sxs-lookup"><span data-stu-id="8ca2b-199">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="8ca2b-200">Создание и изменение маршрутизации для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ca2b-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="8ca2b-201">Связать вашей виртуальной сети tooyour канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8ca2b-201">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

