---
title: "Как настроить маршрутизацию (пиринг) для канала ExpressRoute в Azure (модель Resource Manager) | Документация Майкрософт"
description: "В этой статье описана процедура создания и подготовки частного пиринга, общедоступного пиринга и пиринга Microsoft для канала ExpressRoute, а также показано, как проверить состояние, обновить или удалить пиринги для канала."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 55ccadfea55b8098ee58dcaef942f6ba54093665
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="f5949-104">Создание и изменение пиринга для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f5949-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="f5949-105">В этой статье описано, как создать и администрировать конфигурацию маршрутизации ExpressRoute в модели развертывания Azure Resource Manager, используя портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f5949-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="f5949-106">Вы также сможете проверить состояние, обновить, удалить и отозвать пиринги для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f5949-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="f5949-107">Если вы хотите использовать для работы с каналом другой метод, выберите подходящую статью из списка ниже.</span><span class="sxs-lookup"><span data-stu-id="f5949-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="f5949-108">Предварительные требования для настройки</span><span class="sxs-lookup"><span data-stu-id="f5949-108">Configuration prerequisites</span></span>

* <span data-ttu-id="f5949-109">Прежде чем приступать к настройке, обязательно изучите [предварительные требования](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md) и [рабочие процессы](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="f5949-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="f5949-110">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f5949-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="f5949-111">Приступая к работе, [создайте канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) ; он должен быть затем включен на стороне поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="f5949-111">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="f5949-112">Для выполнения командлетов, описанных в следующих разделах, нужно подготовить и включить канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f5949-112">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in the next sections.</span></span>
* <span data-ttu-id="f5949-113">Если вы планируете использовать общий ключ или хэш MD5, используйте его на обеих сторонах туннеля и ограничьте максимальное число символов до 25.</span><span class="sxs-lookup"><span data-stu-id="f5949-113">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span></span>

<span data-ttu-id="f5949-114">Эти инструкции распространяются только на каналы от поставщиков, предоставляющих услуги подключения второго уровня.</span><span class="sxs-lookup"><span data-stu-id="f5949-114">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="f5949-115">Если ваш поставщик услуг подключения предлагает услуги третьего уровня (обычно это IPVPN, например MPLS), он выполнит настройку маршрутизации и управление ею.</span><span class="sxs-lookup"><span data-stu-id="f5949-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f5949-116">Мы пока не предлагаем использовать пиринги, которые настроены поставщиками услуг на портале управления службами.</span><span class="sxs-lookup"><span data-stu-id="f5949-116">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="f5949-117">Такая возможность будет предоставлена позже.</span><span class="sxs-lookup"><span data-stu-id="f5949-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="f5949-118">Перед настройкой пирингов BGP уточните информацию у поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="f5949-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="f5949-119">Для каждого канала ExpressRoute можно настроить один, два или три пиринга (частный пиринг Azure, общедоступный пиринг Azure и пиринг Microsoft).</span><span class="sxs-lookup"><span data-stu-id="f5949-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="f5949-120">Пиринги можно настраивать в любом порядке,</span><span class="sxs-lookup"><span data-stu-id="f5949-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="f5949-121">главное, выполнять их конфигурацию по очереди.</span><span class="sxs-lookup"><span data-stu-id="f5949-121">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="f5949-122">Частный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="f5949-122">Azure private peering</span></span>

<span data-ttu-id="f5949-123">Этот раздел поможет вам создать, получить, обновить и (или) удалить конфигурацию частного пиринга Azure для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f5949-123">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="f5949-124">Создание частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="f5949-124">To create Azure private peering</span></span>

1. <span data-ttu-id="f5949-125">Настройте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f5949-125">Configure the ExpressRoute circuit.</span></span> <span data-ttu-id="f5949-126">Прежде чем продолжить, убедитесь, что канал полностью подготовлен поставщиком услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="f5949-126">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f5949-128">Настройте для канала частный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="f5949-128">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="f5949-129">Прежде чем продолжить, убедитесь в наличии следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f5949-129">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="f5949-130">Подсеть /30 для основной ссылки.</span><span class="sxs-lookup"><span data-stu-id="f5949-130">A /30 subnet for the primary link.</span></span> <span data-ttu-id="f5949-131">Эта подсеть не должна входить в адресное пространство, зарезервированное для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="f5949-131">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="f5949-132">Подсеть /30 для дополнительной ссылки.</span><span class="sxs-lookup"><span data-stu-id="f5949-132">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="f5949-133">Эта подсеть не должна входить в адресное пространство, зарезервированное для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="f5949-133">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="f5949-134">Действительный идентификатор виртуальной локальной сети для установки пиринга.</span><span class="sxs-lookup"><span data-stu-id="f5949-134">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="f5949-135">Идентификатор не должен использоваться ни одним другим пирингом в канале.</span><span class="sxs-lookup"><span data-stu-id="f5949-135">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="f5949-136">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="f5949-136">AS number for peering.</span></span> <span data-ttu-id="f5949-137">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="f5949-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="f5949-138">Для этого пиринга можно использовать частный номер AS.</span><span class="sxs-lookup"><span data-stu-id="f5949-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="f5949-139">Не используйте номер 65515.</span><span class="sxs-lookup"><span data-stu-id="f5949-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="f5949-140">**Необязательно.** Хэш MD5, если вы решите его использовать.</span><span class="sxs-lookup"><span data-stu-id="f5949-140">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="f5949-141">Выберите в таблице пирингов нужный частный пиринг Azure, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="f5949-141">Select the Azure Private peering row, as shown in the following example:</span></span>

  ![Частный пиринг](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="f5949-143">Настройте частный пиринг.</span><span class="sxs-lookup"><span data-stu-id="f5949-143">Configure private peering.</span></span> <span data-ttu-id="f5949-144">На следующем изображении показан пример настройки:</span><span class="sxs-lookup"><span data-stu-id="f5949-144">The following image shows a configuration example:</span></span>

  ![Настройка частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="f5949-146">Указав все параметры, сохраните конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="f5949-146">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="f5949-147">После подтверждения настройки отобразится примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="f5949-147">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Сохранение частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="f5949-149">Просмотр сведений о частном пиринге Azure</span><span class="sxs-lookup"><span data-stu-id="f5949-149">To view Azure private peering details</span></span>

<span data-ttu-id="f5949-150">Чтобы посмотреть свойства частного пиринга Azure, выберите нужный пиринг.</span><span class="sxs-lookup"><span data-stu-id="f5949-150">You can view the properties of Azure private peering by selecting the peering.</span></span>

![Просмотр частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="f5949-152">Обновление конфигурации частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="f5949-152">To update Azure private peering configuration</span></span>

<span data-ttu-id="f5949-153">Щелкнув строку пиринга, вы сможете изменить свойства пиринга.</span><span class="sxs-lookup"><span data-stu-id="f5949-153">You can select the row for peering and modify the peering properties.</span></span>

![Обновление частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="f5949-155">Удаление частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="f5949-155">To delete Azure private peering</span></span>

<span data-ttu-id="f5949-156">Конфигурацию пиринга можно удалить, щелкнув значок "Удалить", как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="f5949-156">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![Удаление частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="f5949-158">Общедоступный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="f5949-158">Azure public peering</span></span>

<span data-ttu-id="f5949-159">Этот раздел поможет создать, получить, обновить и (или) удалить конфигурацию общедоступного пиринга Azure для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f5949-159">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="f5949-160">Создание общедоступного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="f5949-160">To create Azure public peering</span></span>

1. <span data-ttu-id="f5949-161">Настройте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f5949-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="f5949-162">Прежде чем продолжить, убедитесь, что канал полностью подготовлен поставщиком услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="f5949-162">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![Отображение общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f5949-164">Настройте для канала общедоступный пиринг Azure.</span><span class="sxs-lookup"><span data-stu-id="f5949-164">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="f5949-165">Прежде чем продолжить, убедитесь в наличии следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f5949-165">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="f5949-166">Подсеть /30 для основной ссылки.</span><span class="sxs-lookup"><span data-stu-id="f5949-166">A /30 subnet for the primary link.</span></span> <span data-ttu-id="f5949-167">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="f5949-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="f5949-168">Подсеть /30 для дополнительной ссылки.</span><span class="sxs-lookup"><span data-stu-id="f5949-168">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="f5949-169">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="f5949-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="f5949-170">Действительный идентификатор виртуальной локальной сети для установки пиринга.</span><span class="sxs-lookup"><span data-stu-id="f5949-170">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="f5949-171">Идентификатор не должен использоваться ни одним другим пирингом в канале.</span><span class="sxs-lookup"><span data-stu-id="f5949-171">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="f5949-172">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="f5949-172">AS number for peering.</span></span> <span data-ttu-id="f5949-173">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="f5949-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="f5949-174">**Необязательно.** Хэш MD5, если вы решите его использовать.</span><span class="sxs-lookup"><span data-stu-id="f5949-174">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="f5949-175">Выберите в таблице пирингов нужный общедоступный пиринг Azure, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="f5949-175">Select the Azure public peering row, as shown in the following image:</span></span>

  ![Выбор строки общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="f5949-177">Настройте общедоступный пиринг.</span><span class="sxs-lookup"><span data-stu-id="f5949-177">Configure public peering.</span></span> <span data-ttu-id="f5949-178">На следующем изображении показан пример настройки:</span><span class="sxs-lookup"><span data-stu-id="f5949-178">The following image shows a configuration example:</span></span>

  ![Настройка общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="f5949-180">Указав все параметры, сохраните конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="f5949-180">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="f5949-181">После подтверждения настройки отобразится примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="f5949-181">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Сохранение настройки общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="f5949-183">Просмотр сведений об общедоступном пиринге Azure</span><span class="sxs-lookup"><span data-stu-id="f5949-183">To view Azure public peering details</span></span>

<span data-ttu-id="f5949-184">Чтобы посмотреть свойства общедоступного пиринга Azure, выберите нужный пиринг.</span><span class="sxs-lookup"><span data-stu-id="f5949-184">You can view the properties of Azure public peering by selecting the peering.</span></span>

![Просмотр свойств общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="f5949-186">Обновление конфигурации общедоступного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="f5949-186">To update Azure public peering configuration</span></span>

<span data-ttu-id="f5949-187">Щелкнув строку пиринга, вы сможете изменить свойства пиринга.</span><span class="sxs-lookup"><span data-stu-id="f5949-187">You can select the row for peering and modify the peering properties.</span></span>

![Выбор строки общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="f5949-189">Удаление общедоступного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="f5949-189">To delete Azure public peering</span></span>

<span data-ttu-id="f5949-190">Настройку пиринга можно удалить, щелкнув значок "Удалить", как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="f5949-190">You can remove your peering configuration by selecting the delete icon, as shown in the following example:</span></span>

![Удаление общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="f5949-192">Пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="f5949-192">Microsoft peering</span></span>

<span data-ttu-id="f5949-193">Этот раздел поможет создать, получить, обновить и (или) удалить конфигурацию пиринга Майкрософт для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f5949-193">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5949-194">Пиринг Майкрософт для каналов ExpressRoute, которые были настроены до 1 августа 2017 г., позволяет объявлять все префиксы служб, даже если фильтры маршрутов не определены.</span><span class="sxs-lookup"><span data-stu-id="f5949-194">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="f5949-195">Пиринг Майкрософт для каналов ExpressRoute, настроенных 1 августа 2017 г. или позднее, не будет объявлять префиксы, пока к каналу не будет присоединен фильтр маршрутов.</span><span class="sxs-lookup"><span data-stu-id="f5949-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="f5949-196">Дополнительные сведения см. в руководстве по [настройке фильтра маршрута для пиринга Майкрософт](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f5949-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="f5949-197">Создание пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="f5949-197">To create Microsoft peering</span></span>

1. <span data-ttu-id="f5949-198">Настройте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f5949-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="f5949-199">Прежде чем продолжить, убедитесь, что канал полностью подготовлен поставщиком услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="f5949-199">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![Отображение пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f5949-201">Настройте пиринг Майкрософт для этого канала.</span><span class="sxs-lookup"><span data-stu-id="f5949-201">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="f5949-202">Перед началом работы убедитесь, что у вас есть следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="f5949-202">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="f5949-203">Подсеть /30 для основной ссылки.</span><span class="sxs-lookup"><span data-stu-id="f5949-203">A /30 subnet for the primary link.</span></span> <span data-ttu-id="f5949-204">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="f5949-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="f5949-205">Подсеть /30 для дополнительной ссылки.</span><span class="sxs-lookup"><span data-stu-id="f5949-205">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="f5949-206">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="f5949-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="f5949-207">Действительный идентификатор виртуальной локальной сети для установки пиринга.</span><span class="sxs-lookup"><span data-stu-id="f5949-207">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="f5949-208">Идентификатор не должен использоваться ни одним другим пирингом в канале.</span><span class="sxs-lookup"><span data-stu-id="f5949-208">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="f5949-209">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="f5949-209">AS number for peering.</span></span> <span data-ttu-id="f5949-210">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="f5949-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="f5949-211">Объявленные префиксы: необходимо предоставить список всех префиксов, которые вы планируете объявить во время сеанса BGP.</span><span class="sxs-lookup"><span data-stu-id="f5949-211">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="f5949-212">Допускаются только общедоступные префиксы IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f5949-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="f5949-213">Если вы планируете отправить набор префиксов, их можно оформить в виде списка, разделенного запятыми.</span><span class="sxs-lookup"><span data-stu-id="f5949-213">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="f5949-214">Эти префиксы должны быть зарегистрированы в RIR/IRR на ваше имя.</span><span class="sxs-lookup"><span data-stu-id="f5949-214">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="f5949-215">**Необязательно.** ASN клиента: для объявления префиксов, не зарегистрированных с номером AS для пиринга, можно указать номер AS, с которым они зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="f5949-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="f5949-216">Имя реестра маршрутизации: можно указать RIR/IRR, в котором зарегистрированы номер AS и префиксы.</span><span class="sxs-lookup"><span data-stu-id="f5949-216">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="f5949-217">**Необязательно.** Хэш MD5, если вы решите его использовать.</span><span class="sxs-lookup"><span data-stu-id="f5949-217">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="f5949-218">Вы можете выбрать пиринг, который необходимо настроить, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="f5949-218">You can select the peering you wish to configure, as shown in the following example.</span></span> <span data-ttu-id="f5949-219">Выберите строку пиринга Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f5949-219">Select the Microsoft peering row.</span></span>

  ![Выбор строки пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="f5949-221">Настройте пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f5949-221">Configure Microsoft peering.</span></span> <span data-ttu-id="f5949-222">На следующем изображении показан пример настройки:</span><span class="sxs-lookup"><span data-stu-id="f5949-222">The following image shows a configuration example:</span></span>

  ![Настройка пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="f5949-224">Указав все параметры, сохраните конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="f5949-224">Save the configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="f5949-225">Если для канала будет установлено состояние "Требуется проверка" (как показано на изображении), следует создать запрос в службу поддержки и предоставить сотрудникам поддержки доказательство того, что вы владеете префиксами.</span><span class="sxs-lookup"><span data-stu-id="f5949-225">If your circuit gets to a 'Validation needed' state (as shown in the image), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span></span>

  ![Сохранение настройки пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="f5949-227">Запрос в службу поддержки можно создать непосредственно на портале, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="f5949-227">You can open a support ticket directly from the portal, as shown in the following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="f5949-228">После подтверждения настройки отобразится примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="f5949-228">After the configuration has been accepted successfully, you see something similar to the following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="f5949-229">Просмотр сведений о пиринге Майкрософт</span><span class="sxs-lookup"><span data-stu-id="f5949-229">To view Microsoft peering details</span></span>

<span data-ttu-id="f5949-230">Чтобы посмотреть свойства общедоступного пиринга Azure, выберите нужный пиринг.</span><span class="sxs-lookup"><span data-stu-id="f5949-230">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="f5949-231">Обновление конфигурации пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="f5949-231">To update Microsoft peering configuration</span></span>

<span data-ttu-id="f5949-232">Щелкнув строку пиринга, вы сможете изменить свойства пиринга.</span><span class="sxs-lookup"><span data-stu-id="f5949-232">You can select the row for peering and modify the peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="f5949-233">Удаление пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="f5949-233">To delete Microsoft peering</span></span>

<span data-ttu-id="f5949-234">Конфигурацию пиринга можно удалить, щелкнув значок "Удалить", как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="f5949-234">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="f5949-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5949-235">Next steps</span></span>

<span data-ttu-id="f5949-236">Следующий шаг — [связывание виртуальной сети с каналом ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f5949-236">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="f5949-237">Дополнительную информацию о рабочих процессах ExpressRoute см. в статье [Процедуры ExpressRoute для подготовки каналов и состояний каналов](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="f5949-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="f5949-238">Дополнительную информацию о пиринге канала см. в статье [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="f5949-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="f5949-239">Подробнее о работе с виртуальными сетями см. в статье [Обзор виртуальных сетей](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f5949-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
