---
title: "Как tooconfigure маршрутизации (пиринг) для канала ExpressRoute: диспетчера ресурсов: Azure | Документы Microsoft"
description: "В этой статье содержится описание этапов hello для создания и подготовки hello private, public и Microsoft пиринг канал ExpressRoute. В этой статье также рассказывается, как состояние toocheck hello, обновления или удаления пиринги для своего канала."
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
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="9b426-104">Создание и изменение пиринга для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9b426-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="9b426-105">Эта статья поможет вам создавать и управлять ими конфигурации маршрутизации для канала ExpressRoute в hello портал Azure с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="9b426-106">Можно также проверить состояние hello, update или delete и отзыв пиринги за канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b426-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="9b426-107">Если вы хотите toouse toowork другой метод с ваш канал, выберите статью из hello после списка:</span><span class="sxs-lookup"><span data-stu-id="9b426-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="9b426-108">Предварительные требования для настройки</span><span class="sxs-lookup"><span data-stu-id="9b426-108">Configuration prerequisites</span></span>

* <span data-ttu-id="9b426-109">Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md) страницы hello [требования к маршрутизации](expressroute-routing.md) страницы и hello [рабочих процессов](expressroute-workflows.md) страницы перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="9b426-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="9b426-110">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b426-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="9b426-111">Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="9b426-111">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="9b426-112">Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен для вас toobe может toorun hello командлеты в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-112">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in hello next sections.</span></span>
* <span data-ttu-id="9b426-113">Если планируется toouse общего ключа/MD5-хэш быть toouse убедиться, что это на обеих сторонах hello туннеля и ограничение hello число символов tooa максимум 25.</span><span class="sxs-lookup"><span data-stu-id="9b426-113">If you plan toouse a shared key/MD5 hash, be sure toouse this on both sides of hello tunnel and limit hello number of characters tooa maximum of 25.</span></span>

<span data-ttu-id="9b426-114">Эти инструкции применяются только toocircuits, созданных с помощью предложения службы связи уровня 2 поставщиков услуг.</span><span class="sxs-lookup"><span data-stu-id="9b426-114">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="9b426-115">Если ваш поставщик услуг подключения предлагает услуги третьего уровня (обычно это IPVPN, например MPLS), он выполнит настройку маршрутизации и управление ею.</span><span class="sxs-lookup"><span data-stu-id="9b426-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9b426-116">Мы сейчас не объявляет пиринги настроен поставщиками услуг через портал управления службами hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-116">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="9b426-117">Такая возможность будет предоставлена позже.</span><span class="sxs-lookup"><span data-stu-id="9b426-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="9b426-118">Перед настройкой пирингов BGP уточните информацию у поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="9b426-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="9b426-119">Для каждого канала ExpressRoute можно настроить один, два или три пиринга (частный пиринг Azure, общедоступный пиринг Azure и пиринг Microsoft).</span><span class="sxs-lookup"><span data-stu-id="9b426-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="9b426-120">Пиринги можно настраивать в любом порядке,</span><span class="sxs-lookup"><span data-stu-id="9b426-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="9b426-121">Тем не менее необходимо выполнить настройку hello из каждого из них пиринга одновременно.</span><span class="sxs-lookup"><span data-stu-id="9b426-121">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="9b426-122">Частный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="9b426-122">Azure private peering</span></span>

<span data-ttu-id="9b426-123">Этот раздел поможет вам создать, получить, обновление и удаление hello Azure закрытая конфигурация пиринга канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b426-123">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="9b426-124">toocreate открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="9b426-124">toocreate Azure private peering</span></span>

1. <span data-ttu-id="9b426-125">Настройте канал ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-125">Configure hello ExpressRoute circuit.</span></span> <span data-ttu-id="9b426-126">Убедитесь, что цепь hello полностью подготовлена с поставщиком услуг подключения hello перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="9b426-126">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="9b426-128">Настройка открытого пиринга Azure для hello схемы.</span><span class="sxs-lookup"><span data-stu-id="9b426-128">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="9b426-129">Убедитесь, что hello следующих элементов, прежде чем продолжить hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9b426-129">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="9b426-130">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-130">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="9b426-131">подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="9b426-131">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="9b426-132">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-132">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="9b426-133">подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="9b426-133">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="9b426-134">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="9b426-134">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="9b426-135">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="9b426-135">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="9b426-136">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="9b426-136">AS number for peering.</span></span> <span data-ttu-id="9b426-137">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="9b426-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="9b426-138">Для этого пиринга можно использовать частный номер AS.</span><span class="sxs-lookup"><span data-stu-id="9b426-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="9b426-139">Не используйте номер 65515.</span><span class="sxs-lookup"><span data-stu-id="9b426-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="9b426-140">**Необязательно —** хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="9b426-140">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="9b426-141">Выберите hello Azure закрытого пиринга строки, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="9b426-141">Select hello Azure Private peering row, as shown in hello following example:</span></span>

  ![Частный пиринг](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="9b426-143">Настройте частный пиринг.</span><span class="sxs-lookup"><span data-stu-id="9b426-143">Configure private peering.</span></span> <span data-ttu-id="9b426-144">Следующие изображения Hello показан пример конфигурации:</span><span class="sxs-lookup"><span data-stu-id="9b426-144">hello following image shows a configuration example:</span></span>

  ![Настройка частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="9b426-146">Сохранение конфигурации hello, после того как заданы все параметры.</span><span class="sxs-lookup"><span data-stu-id="9b426-146">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="9b426-147">После успешного принятия конфигурации hello, вы видите что-нибудь подобное toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="9b426-147">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Сохранение частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="9b426-149">tooview Azure закрытого пиринга подробные сведения</span><span class="sxs-lookup"><span data-stu-id="9b426-149">tooview Azure private peering details</span></span>

<span data-ttu-id="9b426-150">Можно просмотреть свойства hello открытого пиринга Azure, выбрав пиринг hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-150">You can view hello properties of Azure private peering by selecting hello peering.</span></span>

![Просмотр частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="9b426-152">tooupdate конфигурации закрытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="9b426-152">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="9b426-153">Можно выбрать строку hello для пиринга и изменить свойства пиринга hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-153">You can select hello row for peering and modify hello peering properties.</span></span>

![Обновление частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="9b426-155">toodelete открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="9b426-155">toodelete Azure private peering</span></span>

<span data-ttu-id="9b426-156">Удалите конфигурацию пиринга, выбрав значок удаления hello, можно, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="9b426-156">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![Удаление частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="9b426-158">Общедоступный пиринг Azure</span><span class="sxs-lookup"><span data-stu-id="9b426-158">Azure public peering</span></span>

<span data-ttu-id="9b426-159">Этот раздел поможет вам создать, получить, обновление и удаление hello Azure открытая конфигурация пиринга канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b426-159">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="9b426-160">toocreate частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="9b426-160">toocreate Azure public peering</span></span>

1. <span data-ttu-id="9b426-161">Настройте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b426-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="9b426-162">Убедитесь, что цепь hello полностью подготовлена с поставщиком услуг подключения hello перед продолжением дальнейшей.</span><span class="sxs-lookup"><span data-stu-id="9b426-162">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![Отображение общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="9b426-164">Настройка открытого пиринга Azure для hello схемы.</span><span class="sxs-lookup"><span data-stu-id="9b426-164">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="9b426-165">Убедитесь, что hello следующих элементов, прежде чем продолжить hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9b426-165">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="9b426-166">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-166">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="9b426-167">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="9b426-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="9b426-168">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-168">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="9b426-169">Это должен быть допустимый префикс общедоступного адреса IPv4.</span><span class="sxs-lookup"><span data-stu-id="9b426-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="9b426-170">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="9b426-170">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="9b426-171">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="9b426-171">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="9b426-172">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="9b426-172">AS number for peering.</span></span> <span data-ttu-id="9b426-173">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="9b426-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="9b426-174">**Необязательно —** хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="9b426-174">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="9b426-175">Выберите hello Azure открытого пиринга строки, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="9b426-175">Select hello Azure public peering row, as shown in hello following image:</span></span>

  ![Выбор строки общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="9b426-177">Настройте общедоступный пиринг.</span><span class="sxs-lookup"><span data-stu-id="9b426-177">Configure public peering.</span></span> <span data-ttu-id="9b426-178">Следующие изображения Hello показан пример конфигурации:</span><span class="sxs-lookup"><span data-stu-id="9b426-178">hello following image shows a configuration example:</span></span>

  ![Настройка общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="9b426-180">Сохранение конфигурации hello, после того как заданы все параметры.</span><span class="sxs-lookup"><span data-stu-id="9b426-180">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="9b426-181">После успешного принятия конфигурации hello, вы видите что-нибудь подобное toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="9b426-181">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Сохранение настройки общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="9b426-183">tooview открытый пиринг сведения о Azure</span><span class="sxs-lookup"><span data-stu-id="9b426-183">tooview Azure public peering details</span></span>

<span data-ttu-id="9b426-184">Можно просмотреть свойства hello открытого пиринга Azure, выбрав пиринг hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-184">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![Просмотр свойств общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="9b426-186">tooupdate конфигурации открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="9b426-186">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="9b426-187">Можно выбрать строку hello для пиринга и изменить свойства пиринга hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-187">You can select hello row for peering and modify hello peering properties.</span></span>

![Выбор строки общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="9b426-189">toodelete частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="9b426-189">toodelete Azure public peering</span></span>

<span data-ttu-id="9b426-190">Пиринга конфигурации можно удалить, выбрав значок удаления hello, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="9b426-190">You can remove your peering configuration by selecting hello delete icon, as shown in hello following example:</span></span>

![Удаление общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="9b426-192">Пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="9b426-192">Microsoft peering</span></span>

<span data-ttu-id="9b426-193">Этот раздел поможет вам создать, получить, обновление и удаление пиринга конфигурации Microsoft hello за канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b426-193">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b426-194">Microsoft пиринг ExpressRoute каналов, которые были настроены предыдущих tooAugust 1, 2017 г. будет иметь все службы префиксов, объявленных через пиринг Майкрософт hello, даже если не определены фильтры маршрутов.</span><span class="sxs-lookup"><span data-stu-id="9b426-194">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="9b426-195">Пиринг каналы ExpressRoute, настроенных в течение или после 1 августа 2017 г. Корпорация Майкрософт не будет иметь префиксы объявленных пока фильтр не будет подключено toohello канала.</span><span class="sxs-lookup"><span data-stu-id="9b426-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="9b426-196">Дополнительные сведения см. в руководстве по [настройке фильтра маршрута для пиринга Майкрософт](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9b426-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="9b426-197">toocreate пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="9b426-197">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="9b426-198">Настройте канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b426-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="9b426-199">Убедитесь, что цепь hello полностью подготовлена с поставщиком услуг подключения hello перед продолжением дальнейшей.</span><span class="sxs-lookup"><span data-stu-id="9b426-199">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![Отображение пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="9b426-201">Настройка Microsoft пиринг для цепи hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-201">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="9b426-202">Убедитесь, что hello следующую информацию, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="9b426-202">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="9b426-203">/ 30 подсеть для основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-203">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="9b426-204">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="9b426-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="9b426-205">/ 30 подсеть для дополнительной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-205">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="9b426-206">Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="9b426-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="9b426-207">Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг.</span><span class="sxs-lookup"><span data-stu-id="9b426-207">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="9b426-208">Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="9b426-208">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="9b426-209">Номер AS для пиринга.</span><span class="sxs-lookup"><span data-stu-id="9b426-209">AS number for peering.</span></span> <span data-ttu-id="9b426-210">Можно использовать 2-байтовые и 4-байтовые номера AS.</span><span class="sxs-lookup"><span data-stu-id="9b426-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="9b426-211">Объявленные префиксы: необходимо предоставить список всех префиксов планирование tooadvertise сеансом BGP hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-211">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="9b426-212">Допускаются только общедоступные префиксы IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="9b426-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="9b426-213">Если планируется toosend набор префиксов, вы можете отправить список с разделителями запятыми.</span><span class="sxs-lookup"><span data-stu-id="9b426-213">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="9b426-214">Эти префиксы должны быть tooyou, зарегистрированные в RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="9b426-214">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="9b426-215">**Необязательно —** клиента ASN: если префиксы рекламы, не зарегистрированный toohello пиринг как число, можно указать hello в качестве номера toowhich они зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="9b426-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="9b426-216">Имя реестра маршрутизации: Можно указать hello RIR / IRR, для какой hello, а число и префиксы зарегистрирована.</span><span class="sxs-lookup"><span data-stu-id="9b426-216">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="9b426-217">**Необязательно —** хэш MD5 при выборе toouse один.</span><span class="sxs-lookup"><span data-stu-id="9b426-217">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="9b426-218">Можно выбрать hello пиринг нужно tooconfigure, как показано в следующих hello пример.</span><span class="sxs-lookup"><span data-stu-id="9b426-218">You can select hello peering you wish tooconfigure, as shown in hello following example.</span></span> <span data-ttu-id="9b426-219">Выберите строку пиринг Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-219">Select hello Microsoft peering row.</span></span>

  ![Выбор строки пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="9b426-221">Настройте пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9b426-221">Configure Microsoft peering.</span></span> <span data-ttu-id="9b426-222">Следующие изображения Hello показан пример конфигурации:</span><span class="sxs-lookup"><span data-stu-id="9b426-222">hello following image shows a configuration example:</span></span>

  ![Настройка пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="9b426-224">Сохранение конфигурации hello, после того как заданы все параметры.</span><span class="sxs-lookup"><span data-stu-id="9b426-224">Save hello configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="9b426-225">Если ваш канал возвращает tooa «Проверка необходимости» состояние (как показано на рисунке hello), необходимо открыть поддержки билет tooshow, подтверждения владения группы поддержки tooour префиксы hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-225">If your circuit gets tooa 'Validation needed' state (as shown in hello image), you must open a support ticket tooshow proof of ownership of hello prefixes tooour support team.</span></span>

  ![Сохранение настройки пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="9b426-227">Непосредственно из портала hello, можно открыть запрос в службу поддержки, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="9b426-227">You can open a support ticket directly from hello portal, as shown in hello following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="9b426-228">После конфигурации hello успешно принято, вы видите что-нибудь подобное toohello после изображения:</span><span class="sxs-lookup"><span data-stu-id="9b426-228">After hello configuration has been accepted successfully, you see something similar toohello following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="9b426-229">данные пиринга tooview Microsoft</span><span class="sxs-lookup"><span data-stu-id="9b426-229">tooview Microsoft peering details</span></span>

<span data-ttu-id="9b426-230">Можно просмотреть свойства hello открытого пиринга Azure, выбрав пиринг hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-230">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="9b426-231">Конфигурация пиринга Майкрософт tooupdate</span><span class="sxs-lookup"><span data-stu-id="9b426-231">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="9b426-232">Можно выбрать строку hello для пиринга и изменить свойства пиринга hello.</span><span class="sxs-lookup"><span data-stu-id="9b426-232">You can select hello row for peering and modify hello peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="9b426-233">toodelete пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="9b426-233">toodelete Microsoft peering</span></span>

<span data-ttu-id="9b426-234">Удалите конфигурацию пиринга, выбрав значок удаления hello, можно, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="9b426-234">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="9b426-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9b426-235">Next steps</span></span>

<span data-ttu-id="9b426-236">Следующий шаг [связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="9b426-236">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="9b426-237">Дополнительную информацию о рабочих процессах ExpressRoute см. в статье [Процедуры ExpressRoute для подготовки каналов и состояний каналов](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="9b426-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="9b426-238">Дополнительную информацию о пиринге канала см. в статье [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="9b426-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="9b426-239">Подробнее о работе с виртуальными сетями см. в статье [Обзор виртуальных сетей](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b426-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
