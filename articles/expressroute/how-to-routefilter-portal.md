---
title: "Настройка фильтров маршрутов для пиринга Azure ExpressRoute Майкрософт | Документация Майкрософт"
description: "В этой статье описывается, как фильтры маршрутов tooconfigure по использованию Microsoft Пиринга hello портал Azure"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="6b38a-103">Настройка фильтров маршрутов для пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="6b38a-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="6b38a-104">Фильтры маршрутов являются способом tooconsume подмножество поддерживаемых услуг через пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6b38a-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="6b38a-105">Hello шаги, приведенные в этой статье справки можно настраивать и управлять фильтры маршрутов для каналов ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b38a-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="6b38a-106">Службы Dynamics 365 и службам Office 365, такие как Exchange Online, SharePoint Online и Скайп для бизнеса, доступны через пиринг Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="6b38a-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="6b38a-107">При настройке пиринг Майкрософт в канал ExpressRoute, через сеансов BGP hello, установленных объявления все префиксы toothese связанных служб.</span><span class="sxs-lookup"><span data-stu-id="6b38a-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="6b38a-108">Значение сообщества BGP является hello вложенного tooevery префикс tooidentify службы, предлагаемые hello префикс.</span><span class="sxs-lookup"><span data-stu-id="6b38a-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="6b38a-109">Список значений сообщества BGP hello и hello служб, они сопоставляются. в разделе [BGP сообщества](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="6b38a-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="6b38a-110">Если необходимо использовать службы связи tooall, большое число префиксов разглашаемые BGP.</span><span class="sxs-lookup"><span data-stu-id="6b38a-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="6b38a-111">Это значительно увеличивает размер hello таблиц маршрутов hello обслуживается маршрутизаторов в сети.</span><span class="sxs-lookup"><span data-stu-id="6b38a-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="6b38a-112">Если планируется tooconsume только подмножество служб, предлагаемым через пиринг Майкрософт, можно уменьшить размер hello таблиц маршрутизации двумя способами.</span><span class="sxs-lookup"><span data-stu-id="6b38a-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="6b38a-113">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="6b38a-113">You can:</span></span>

- <span data-ttu-id="6b38a-114">Отфильтровывать нежелательные префиксы путем применения фильтров маршрутов к сообществам BGP.</span><span class="sxs-lookup"><span data-stu-id="6b38a-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="6b38a-115">Это стандартная сетевая практика и обычно используется во многих сетях.</span><span class="sxs-lookup"><span data-stu-id="6b38a-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="6b38a-116">Определение фильтров маршрута и применить их tooyour канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b38a-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="6b38a-117">Фильтр — новый ресурс, что позволяет выбрать hello список служб, которые планирование tooconsume через пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6b38a-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="6b38a-118">ExpressRoute они передают лишь hello список префиксов, которые принадлежат toohello службы, определенные в фильтре hello маршрута.</span><span class="sxs-lookup"><span data-stu-id="6b38a-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="6b38a-119"><a name="about"></a>О фильтрах маршрута</span><span class="sxs-lookup"><span data-stu-id="6b38a-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="6b38a-120">Когда пиринг Майкрософт настроена на ваш канал ExpressRoute, периметрическими маршрутизаторами Microsoft hello установить паре сеансов BGP с маршрутизаторами edge hello (вашим или поставщика услуг подключения).</span><span class="sxs-lookup"><span data-stu-id="6b38a-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="6b38a-121">Маршруты, объявленные tooyour сети.</span><span class="sxs-lookup"><span data-stu-id="6b38a-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="6b38a-122">tooenable объявления tooyour маршруте, необходимо связать фильтр маршрутов.</span><span class="sxs-lookup"><span data-stu-id="6b38a-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="6b38a-123">Фильтр позволяет выявить службы будут tooconsume через пиринг Майкрософт канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b38a-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="6b38a-124">Это по сути белый список значений всех hello BGP сообщества.</span><span class="sxs-lookup"><span data-stu-id="6b38a-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="6b38a-125">После определен и присоединенного tooan канал ExpressRoute ресурса фильтров маршрута, все префиксы, сопоставленные toohello BGP сообщества значения являются объявленной tooyour сети.</span><span class="sxs-lookup"><span data-stu-id="6b38a-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="6b38a-126">фильтры маршрутов может tooattach toobe со службами Office 365 на них, необходимо иметь авторизации служб Office 365 tooconsume через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b38a-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="6b38a-127">При отсутствии службы авторизованным tooconsume Office 365 с помощью ExpressRoute, фильтры маршрутов tooattach hello операция завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="6b38a-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="6b38a-128">Дополнительные сведения о процессе авторизации hello см. в разделе [ExpressRoute Azure для Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="6b38a-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="6b38a-129">Службы 365 tooDynamics связи не требуется никакой предыдущих авторизации.</span><span class="sxs-lookup"><span data-stu-id="6b38a-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b38a-130">Microsoft пиринг ExpressRoute каналов, которые были настроены предыдущих tooAugust 1, 2017 г. будет иметь все службы префиксов, объявленных через пиринг Майкрософт, даже если не определены фильтры маршрутов.</span><span class="sxs-lookup"><span data-stu-id="6b38a-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="6b38a-131">Пиринг каналы ExpressRoute, настроенных в течение или после 1 августа 2017 г. Корпорация Майкрософт не будет иметь префиксы объявленных пока фильтр не будет подключено toohello канала.</span><span class="sxs-lookup"><span data-stu-id="6b38a-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="6b38a-132"><a name="workflow"></a>Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="6b38a-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="6b38a-133">возможности toosuccessfully toobe подключение tooservices через пиринг Майкрософт, необходимо выполнить следующие действия по настройке hello:</span><span class="sxs-lookup"><span data-stu-id="6b38a-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="6b38a-134">Необходимо иметь активный канал ExpressRoute с подготовленным пирингом Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6b38a-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="6b38a-135">Эти задачи можно использовать следующие инструкции tooaccomplish hello:</span><span class="sxs-lookup"><span data-stu-id="6b38a-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="6b38a-136">[Создайте канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="6b38a-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="6b38a-137">Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен.</span><span class="sxs-lookup"><span data-stu-id="6b38a-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="6b38a-138">[Создайте пиринг Майкрософт](expressroute-howto-routing-portal-resource-manager.md) при управлении hello непосредственно в сеансе BGP.</span><span class="sxs-lookup"><span data-stu-id="6b38a-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="6b38a-139">или если у вашего поставщика услуг подключения подготовлен пиринг Майкрософт для вашего канала.</span><span class="sxs-lookup"><span data-stu-id="6b38a-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="6b38a-140">Необходимо создать и настроить фильтр маршрутов.</span><span class="sxs-lookup"><span data-stu-id="6b38a-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="6b38a-141">Определите hello сервисы tooconsume через пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="6b38a-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="6b38a-142">Определить hello список значений BGP сообщества, связанные со службами hello</span><span class="sxs-lookup"><span data-stu-id="6b38a-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="6b38a-143">Создать правило tooallow hello префикс список сопоставления hello значения BGP сообщества</span><span class="sxs-lookup"><span data-stu-id="6b38a-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="6b38a-144">Необходимо добавить канал ExpressRoute toohello фильтра маршрута hello.</span><span class="sxs-lookup"><span data-stu-id="6b38a-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6b38a-145">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="6b38a-145">Before you begin</span></span>

<span data-ttu-id="6b38a-146">Перед началом настройки убедитесь, что соблюдены следующие условия hello:</span><span class="sxs-lookup"><span data-stu-id="6b38a-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="6b38a-147">Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="6b38a-147">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="6b38a-148">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b38a-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="6b38a-149">Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="6b38a-149">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="6b38a-150">Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен.</span><span class="sxs-lookup"><span data-stu-id="6b38a-150">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="6b38a-151">Необходимо иметь активный пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6b38a-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="6b38a-152">Следуйте инструкциям в статье [Создание и изменение канала ExpressRoute с помощью PowerShell](expressroute-howto-routing-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6b38a-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="6b38a-153"><a name="prefixes"></a>Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="6b38a-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="6b38a-154">Получение списка префиксов и значений сообщества BGP</span><span class="sxs-lookup"><span data-stu-id="6b38a-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="6b38a-155">1. Получение списка значений сообщества BGP</span><span class="sxs-lookup"><span data-stu-id="6b38a-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="6b38a-156">Значения BGP сообщества, связанные со службами, доступными через пиринг Майкрософт доступна в hello [требования к маршрутизации ExpressRoute](expressroute-routing.md) страницы.</span><span class="sxs-lookup"><span data-stu-id="6b38a-156">BGP community values associated with services accessible through Microsoft peering is available in hello [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="6b38a-157">2. Создайте список значений hello, которые должны toouse</span><span class="sxs-lookup"><span data-stu-id="6b38a-157">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="6b38a-158">Составьте список нужные значения сообщества BGP toouse в фильтре hello маршрута.</span><span class="sxs-lookup"><span data-stu-id="6b38a-158">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="6b38a-159">Например значение сообщества BGP для службы Dynamics 365 hello — 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="6b38a-159">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="6b38a-160"><a name="filter"></a>Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="6b38a-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="6b38a-161">Создание фильтра маршрута и правила фильтрации</span><span class="sxs-lookup"><span data-stu-id="6b38a-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="6b38a-162">Фильтр может иметь только одно правило и hello правило должно иметь тип «Разрешить».</span><span class="sxs-lookup"><span data-stu-id="6b38a-162">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="6b38a-163">С этим правилом может быть связан список значений сообщества BGP.</span><span class="sxs-lookup"><span data-stu-id="6b38a-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="6b38a-164">1. Создание фильтра маршрута</span><span class="sxs-lookup"><span data-stu-id="6b38a-164">1. Create a route filter</span></span>
<span data-ttu-id="6b38a-165">Можно создать фильтр, выбрав параметр toocreate hello новый ресурс.</span><span class="sxs-lookup"><span data-stu-id="6b38a-165">You can create a route filter by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="6b38a-166">Нажмите кнопку **New** > **сети** > **RouteFilter**, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="6b38a-166">Click **New** > **Networking** > **RouteFilter**, as shown in hello following image:</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="6b38a-168">Фильтр маршрутов hello необходимо разместить в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6b38a-168">You must place hello route filter in a resource group.</span></span> 

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="6b38a-170">2. Создание правила фильтрации</span><span class="sxs-lookup"><span data-stu-id="6b38a-170">2. Create a filter rule</span></span>

<span data-ttu-id="6b38a-171">Можно добавить и на вкладке правила фильтра маршрута управление правила обновления, выбрав hello.</span><span class="sxs-lookup"><span data-stu-id="6b38a-171">You can add and update rules by selecting hello manage rule tab for your route filter.</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="6b38a-173">Вы можете выбрать hello службы будут tooconnect toofrom hello раскрывающегося списка и сохранить правило hello после завершения.</span><span class="sxs-lookup"><span data-stu-id="6b38a-173">You can select hello services you want tooconnect toofrom hello drop down list and save hello rule when done.</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="6b38a-175"><a name="attach"></a>Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="6b38a-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="6b38a-176">Присоединение канал ExpressRoute tooan фильтра маршрута hello</span><span class="sxs-lookup"><span data-stu-id="6b38a-176">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="6b38a-177">Можно присоединить hello маршрута фильтра tooa цепи, нужно нажать кнопку «Добавить канал» hello и выбрав канал ExpressRoute hello hello раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="6b38a-177">You can attach hello route filter tooa circuit by selecting hello "add Circuit" button and selecting hello ExpressRoute circuit from hello drop down list.</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="6b38a-179"><a name="getproperties"></a>свойства hello tooget фильтра маршрута</span><span class="sxs-lookup"><span data-stu-id="6b38a-179"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="6b38a-180">При открытии ресурса hello hello портала можно просмотреть свойства фильтра маршрута.</span><span class="sxs-lookup"><span data-stu-id="6b38a-180">You can view properties of a route filter when you open hello resource in hello portal.</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="6b38a-182"><a name="updateproperties"></a>свойства hello tooupdate фильтра маршрута</span><span class="sxs-lookup"><span data-stu-id="6b38a-182"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="6b38a-183">Нажав кнопку "hello «управление правило»" можно обновить список hello BGP сообщества значения вложенного tooa канала.</span><span class="sxs-lookup"><span data-stu-id="6b38a-183">You can update hello list of BGP community values attached tooa circuit by selecting hello "Manage rule" button.</span></span>


![Создание фильтра маршрута](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="6b38a-186"><a name="detach"></a>toodetach фильтр маршрутов из канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6b38a-186"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="6b38a-187">toodetach канала из фильтра маршрута hello, щелкните правой кнопкой мыши в цепи hello и выберите команду «Отменить связь».</span><span class="sxs-lookup"><span data-stu-id="6b38a-187">toodetach a circuit from hello route filter, right click on hello circuit and click on "disassociate".</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="6b38a-189"><a name="delete"></a>toodelete фильтр маршрутов</span><span class="sxs-lookup"><span data-stu-id="6b38a-189"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="6b38a-190">Фильтр можно удалить, нажав кнопку "Удалить" hello.</span><span class="sxs-lookup"><span data-stu-id="6b38a-190">You can delete a route filter by selecting hello delete button.</span></span> 

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="6b38a-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b38a-192">Next steps</span></span>

<span data-ttu-id="6b38a-193">Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="6b38a-193">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
