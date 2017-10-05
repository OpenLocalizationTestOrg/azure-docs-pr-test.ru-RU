---
title: "Создание и изменение канала ExpressRoute с помощью портала Azure | Документация Майкрософт"
description: "В этой статье описывается создание, подготовка, проверка, обновление, удаление и отзыв канала ExpressRoute."
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
ms.openlocfilehash: e3721cd3c031622788f553e71a6555b844f3f7dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="7d98a-103">Создание и изменение канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7d98a-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d98a-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="7d98a-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="7d98a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d98a-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="7d98a-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="7d98a-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="7d98a-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="7d98a-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="7d98a-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="7d98a-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="7d98a-109">В этой статье объясняется, как создать канал Azure ExpressRoute, используя портал Azure и модель развертывания с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7d98a-109">This article describes how to create an Azure ExpressRoute circuit by using the Azure portal and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="7d98a-110">Описанные ниже действия показывают, как проверить состояние канала, обновить его или удалить и отозвать.</span><span class="sxs-lookup"><span data-stu-id="7d98a-110">The following steps also show you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="7d98a-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="7d98a-111">Before you begin</span></span>
* <span data-ttu-id="7d98a-112">Изучите [предварительные требования](expressroute-prerequisites.md) и [рабочие процессы](expressroute-workflows.md), прежде чем приступить к настройке.</span><span class="sxs-lookup"><span data-stu-id="7d98a-112">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="7d98a-113">Убедитесь в том, что у вас есть доступ к [порталу Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d98a-113">Ensure that you have access to the [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="7d98a-114">Убедитесь в том, что у вас есть разрешения на создание сетевых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7d98a-114">Ensure that you have permissions to create new networking resources.</span></span> <span data-ttu-id="7d98a-115">Если у вас нет нужных разрешений, обратитесь к администратору учетной записи.</span><span class="sxs-lookup"><span data-stu-id="7d98a-115">Contact your account administrator if you do not have the right permissions.</span></span>
* <span data-ttu-id="7d98a-116">Вы можете [просмотреть видео](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit), прежде чем начать, чтобы лучше понять выполняемые действия.</span><span class="sxs-lookup"><span data-stu-id="7d98a-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order to better understand the steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="7d98a-117">Создание и предоставление канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7d98a-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-the-azure-portal"></a><span data-ttu-id="7d98a-118">1. Выполните вход на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7d98a-118">1. Sign in to the Azure portal</span></span>
<span data-ttu-id="7d98a-119">В браузере откройте [портал Azure](http://portal.azure.com) и выполните вход с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="7d98a-119">From a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="7d98a-120">2. Создание канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7d98a-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7d98a-121">Выставление счетов за использование ExpressRoute начинается после того, как клиент получает служебный ключ.</span><span class="sxs-lookup"><span data-stu-id="7d98a-121">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="7d98a-122">Обязательно выполните эту операцию, как только поставщик услуг подключения будет готов предоставить канал.</span><span class="sxs-lookup"><span data-stu-id="7d98a-122">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

1. <span data-ttu-id="7d98a-123">Чтобы создать канал ExpressRoute, можно выбрать команду создания ресурса.</span><span class="sxs-lookup"><span data-stu-id="7d98a-123">You can create an ExpressRoute circuit by selecting the option to create a new resource.</span></span> <span data-ttu-id="7d98a-124">Выберите **Создать** > **Сети** > **ExpressRoute**, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="7d98a-124">Click **New** > **Networking** > **ExpressRoute**, as shown in the following image:</span></span>
   
    ![Создание канала ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="7d98a-126">После щелчка **ExpressRoute** отобразится колонка **Создание канала ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="7d98a-126">After you click **ExpressRoute**, you'll see the **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="7d98a-127">При заполнении значений в этой колонке необходимо указать правильный уровень SKU и измерение данных.</span><span class="sxs-lookup"><span data-stu-id="7d98a-127">When you're filling in the values on this blade, make sure that you specify the correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="7d98a-128">**Уровень** определяет, какого уровня надстройка включена — ExpressRoute "Стандартный" или ExpressRoute "Премиум".</span><span class="sxs-lookup"><span data-stu-id="7d98a-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="7d98a-129">Укажите **Standard**, чтобы получить SKU Standard, или **Premium**, чтобы получить надстройку Premium.</span><span class="sxs-lookup"><span data-stu-id="7d98a-129">You can specify **Standard** to get the standard SKU or **Premium** for the premium add-on.</span></span>
   * <span data-ttu-id="7d98a-130">**Измерение данных** определяет тип выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="7d98a-130">**Data metering** determines the billing type.</span></span> <span data-ttu-id="7d98a-131">Выберите **С учетом трафика** для тарифного плана с оплатой за трафик или **Не ограничено** для безлимитного тарифного плана.</span><span class="sxs-lookup"><span data-stu-id="7d98a-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="7d98a-132">Обратите внимание, что тип выставления счетов можно изменить со **С учетом трафика** на **Не ограничено**, но не наоборот. **Не ограничено****С учетом трафика**</span><span class="sxs-lookup"><span data-stu-id="7d98a-132">Note that you can change the billing type from **Metered** to **Unlimited**, but you can't change the type from **Unlimited** to **Metered**.</span></span>
     
     ![Настройка уровня SKU и измерения данных](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="7d98a-134">Имейте в виду, что "Расположение пиринга" указывает [физическое расположение](expressroute-locations.md) пиринга с корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7d98a-134">Please be aware that the Peering Location indicates the [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="7d98a-135">Оно **не** связано со свойством Location, которое ссылается на географический регион, в котором находится поставщик сетевых ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="7d98a-135">This is **not** linked to "Location" property, which refers to the geography where the Azure Network Resource Provider is located.</span></span> <span data-ttu-id="7d98a-136">Хотя они не связаны, рекомендуется выбрать поставщик сетевых ресурсов, находящийся недалеко от расположения пиринга канала.</span><span class="sxs-lookup"><span data-stu-id="7d98a-136">While they are not related, it is a good practice to choose a Network Resource Provider geographically close to the Peering Location of the circuit.</span></span> 
> 
> 

### <a name="3-view-the-circuits-and-properties"></a><span data-ttu-id="7d98a-137">3. Просмотр каналов и свойств</span><span class="sxs-lookup"><span data-stu-id="7d98a-137">3. View the circuits and properties</span></span>
<span data-ttu-id="7d98a-138">**Просмотр всех каналов**</span><span class="sxs-lookup"><span data-stu-id="7d98a-138">**View all the circuits**</span></span>

<span data-ttu-id="7d98a-139">Вы можете просмотреть все созданные вами каналы, выбрав в меню слева пункт **Все ресурсы** .</span><span class="sxs-lookup"><span data-stu-id="7d98a-139">You can view all the circuits that you created by selecting **All resources** on the left-side menu.</span></span>

![Просмотр каналов](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="7d98a-141">**Просмотр свойств**</span><span class="sxs-lookup"><span data-stu-id="7d98a-141">**View the properties**</span></span>

    You can view the properties of the circuit by selecting it. On this blade, note the service key for the circuit. You must copy the circuit key for your circuit and pass it down to the service provider to complete the provisioning process. The circuit key is specific to your circuit.

![Свойства](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="7d98a-143">4. Отправка ключа службы поставщику услуг подключения для подготовки</span><span class="sxs-lookup"><span data-stu-id="7d98a-143">4. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="7d98a-144">В этой колонке параметр **Состояние поставщика** предоставляет сведения о текущем состоянии подготовки на стороне поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="7d98a-144">On this blade, **Provider status** provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="7d98a-145">Параметр **Состояние цепи** предоставляет состояние на стороне инфраструктуры Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7d98a-145">**Circuit status** provides the state on the Microsoft side.</span></span> <span data-ttu-id="7d98a-146">Дополнительные сведения о состояниях подготовки канала см. в статье [Рабочие процессы](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="7d98a-146">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="7d98a-147">Вновь созданный канал ExpressRoute будет иметь следующее состояние:</span><span class="sxs-lookup"><span data-stu-id="7d98a-147">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

<span data-ttu-id="7d98a-148">Состояние поставщика: Не подготовлено</span><span class="sxs-lookup"><span data-stu-id="7d98a-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="7d98a-149">Состояние канала: Включен</span><span class="sxs-lookup"><span data-stu-id="7d98a-149">Circuit status: Enabled</span></span>

![Инициация процесса подготовки](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="7d98a-151">Когда поставщик услуг подключения находится в процессе его активации, канал переходит в следующее состояние:</span><span class="sxs-lookup"><span data-stu-id="7d98a-151">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

<span data-ttu-id="7d98a-152">Состояние поставщика: Идет подготовка</span><span class="sxs-lookup"><span data-stu-id="7d98a-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="7d98a-153">Состояние канала: Включен</span><span class="sxs-lookup"><span data-stu-id="7d98a-153">Circuit status: Enabled</span></span>

<span data-ttu-id="7d98a-154">Для того чтобы канал ExpressRoute можно было использовать, он должен находиться в следующем состоянии:</span><span class="sxs-lookup"><span data-stu-id="7d98a-154">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

<span data-ttu-id="7d98a-155">Состояние поставщика: Подготовлено</span><span class="sxs-lookup"><span data-stu-id="7d98a-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="7d98a-156">Состояние канала: Включен</span><span class="sxs-lookup"><span data-stu-id="7d98a-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="7d98a-157">5. Периодическая проверка состояния и статуса ключа канала</span><span class="sxs-lookup"><span data-stu-id="7d98a-157">5. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="7d98a-158">Чтобы просмотреть свойства интересующего вас канала, выберите его.</span><span class="sxs-lookup"><span data-stu-id="7d98a-158">You can view the properties of the circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="7d98a-159">Проверьте **Состояние поставщика**. Чтобы вы могли продолжить работу, оно должно измениться на **Подготовлено**.</span><span class="sxs-lookup"><span data-stu-id="7d98a-159">Check the **Provider status** and ensure that it has moved to **Provisioned** before you continue.</span></span>

![Состояние канала и поставщика](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="7d98a-161">6. Создание конфигурации маршрутизации</span><span class="sxs-lookup"><span data-stu-id="7d98a-161">6. Create your routing configuration</span></span>
<span data-ttu-id="7d98a-162">Пошаговые инструкции по созданию и изменению пиринга каналов см. в статье [Создание и изменение маршрутизации для канала ExpressRoute](expressroute-howto-routing-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7d98a-162">For step-by-step instructions, refer to the [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d98a-163">Эти инструкции распространяются только на каналы от поставщиков, предоставляющих услуги подключения второго уровня.</span><span class="sxs-lookup"><span data-stu-id="7d98a-163">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="7d98a-164">Если вы работаете с поставщиком, предлагающим услуги третьего уровня (обычно это IPVPN, например MPLS), то ваш поставщик услуг подключения выполнит настройку и управление конфигурацией самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="7d98a-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="7d98a-165">7. Связывание виртуальной сети с каналом ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7d98a-165">7. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="7d98a-166">Теперь свяжите виртуальную сеть с каналом ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7d98a-166">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="7d98a-167">При работе с моделью развертывания Resource Manager пользуйтесь статьей [Связывание виртуальной сети с каналом ExpressRoute](expressroute-howto-linkvnet-arm.md) .</span><span class="sxs-lookup"><span data-stu-id="7d98a-167">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="7d98a-168">Получение состояния канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7d98a-168">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="7d98a-169">Чтобы просмотреть состояние канала, выберите его.</span><span class="sxs-lookup"><span data-stu-id="7d98a-169">You can view the status of a circuit by selecting it.</span></span> 

![Состояние канала ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="7d98a-171">Изменение канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7d98a-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="7d98a-172">Некоторые свойства канала ExpressRoute можно изменить, не повлияв на подключение.</span><span class="sxs-lookup"><span data-stu-id="7d98a-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="7d98a-173">Вы можете выполнять следующие действия без простоя:</span><span class="sxs-lookup"><span data-stu-id="7d98a-173">You can do the following with no downtime:</span></span>

* <span data-ttu-id="7d98a-174">включать и отключать надстройку ExpressRoute "Премиум" для канала ExpressRoute;</span><span class="sxs-lookup"><span data-stu-id="7d98a-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="7d98a-175">увеличивать пропускную способность канала ExpressRoute при условии, что в порту имеется доступная емкость.</span><span class="sxs-lookup"><span data-stu-id="7d98a-175">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="7d98a-176">Обратите внимание, что снижение пропускной способности канала не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7d98a-176">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="7d98a-177">Перейдите с тарифного плана с оплатой за трафик на безлимитный тарифный план.</span><span class="sxs-lookup"><span data-stu-id="7d98a-177">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="7d98a-178">Обратите внимание, что переход с безлимитного тарифного плана на тарифный план с оплатой за трафик не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7d98a-178">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="7d98a-179">Параметр *Allow Classic Operations*(Разрешить классические операции) можно включать и отключать.</span><span class="sxs-lookup"><span data-stu-id="7d98a-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="7d98a-180">Дополнительные сведения об ограничениях см. в статье [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="7d98a-180">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="7d98a-181">Чтобы изменить канал ExpressRoute, щелкните **Конфигурация**, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="7d98a-181">To modify an ExpressRoute circuit, click on the **Configuration** as shown in the figure below.</span></span>

![Изменение канала](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="7d98a-183">В колонке "Конфигурация" можно изменить пропускную способность, номер SKU, модель выставления счетов и разрешить классические операции.</span><span class="sxs-lookup"><span data-stu-id="7d98a-183">You can modify the bandwidth, SKU, billing model and allow classic operations within the configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d98a-184">Может потребоваться заново создать канал ExpressRoute, если существующий порт не обеспечивает достаточную емкость.</span><span class="sxs-lookup"><span data-stu-id="7d98a-184">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="7d98a-185">Канал невозможно обновить, если в его расположении нет доступной дополнительной емкости.</span><span class="sxs-lookup"><span data-stu-id="7d98a-185">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="7d98a-186">Уменьшить пропускную способность канала ExpressRoute без прерывания его работы нельзя.</span><span class="sxs-lookup"><span data-stu-id="7d98a-186">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="7d98a-187">Для снижения пропускной способности нужно будет отозвать канал ExpressRoute и повторно подготовить новый канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7d98a-187">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="7d98a-188">Отключение надстройки уровня "Премиум" может завершиться ошибкой, если используется больше ресурсов, чем разрешено для канала уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="7d98a-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="7d98a-189">Отзыв и удаление канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7d98a-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="7d98a-190">Канал ExpressRoute можно удалить, щелкнув значок **Удалить** .</span><span class="sxs-lookup"><span data-stu-id="7d98a-190">You can delete your ExpressRoute circuit by selecting the **delete** icon.</span></span> <span data-ttu-id="7d98a-191">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="7d98a-191">Note the following:</span></span>

* <span data-ttu-id="7d98a-192">Связь между ExpressRoute и всеми виртуальными сетями необходимо разорвать.</span><span class="sxs-lookup"><span data-stu-id="7d98a-192">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="7d98a-193">Если операция завершится ошибкой, проверьте, не привязаны ли к каналу какие-либо виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="7d98a-193">If this operation fails, check whether any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="7d98a-194">Если подготовка поставщика услуг канала ExpressRoute находится в состоянии **Идет подготовка** или **Подготовлено** то свяжитесь с поставщиком услуг, чтобы отозвать канал с его стороны.</span><span class="sxs-lookup"><span data-stu-id="7d98a-194">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="7d98a-195">Мы будем резервировать ресурсы и выставлять вам счета до тех пор, пока поставщик услуг не завершит отзыв канала и не отправит нам соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="7d98a-195">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="7d98a-196">Если поставщик услуг отзовет канал (состояние подготовки поставщика услуг изменится на **Не подготовлено**), то вы можете удалить канал.</span><span class="sxs-lookup"><span data-stu-id="7d98a-196">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="7d98a-197">В результате будет приостановлено выставление счетов за этот канал.</span><span class="sxs-lookup"><span data-stu-id="7d98a-197">This will stop billing for the circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d98a-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7d98a-198">Next steps</span></span>
<span data-ttu-id="7d98a-199">После создания канала обязательно выполните действия, описанные в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="7d98a-199">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="7d98a-200">Создание и изменение маршрутизации для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7d98a-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="7d98a-201">Связывание виртуальной сети с каналом ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7d98a-201">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

