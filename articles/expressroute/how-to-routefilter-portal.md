---
title: "Настройка фильтров маршрутов для пиринга Azure ExpressRoute Майкрософт | Документация Майкрософт"
description: "В этой статье описывается, как настраивать фильтры маршрутов для пиринга Майкрософт с помощью портала Azure"
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
ms.openlocfilehash: f17bf3e475a33cfc617e8a026e9606b3792101f3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="375eb-103">Настройка фильтров маршрутов для пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="375eb-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="375eb-104">Фильтры маршрутов — это способ использовать подмножество поддерживаемых служб через пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="375eb-104">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="375eb-105">Действия, описанные в этой статье, помогут настроить фильтры маршрутов для каналов ExpressRoute и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="375eb-105">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="375eb-106">Службы Dynamics 365 и службы Office 365, такие как Exchange Online, SharePoint Online и Skype для бизнеса, доступны через пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="375eb-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="375eb-107">При настройке пиринга Майкрософт в канале ExpressRoute все префиксы, которые относятся к этим службам, объявляются через установленные сеансы BGP.</span><span class="sxs-lookup"><span data-stu-id="375eb-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="375eb-108">Значение сообщества BGP подключается к каждому префиксу для идентификации службы, предлагаемой через него.</span><span class="sxs-lookup"><span data-stu-id="375eb-108">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="375eb-109">Список значений сообщества BGP и служб, с которыми они сопоставляются, см. в разделе [Поддержка сообществ BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="375eb-109">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="375eb-110">Если требуется подключение ко всем службам, большое число префиксов объявляется через BGP.</span><span class="sxs-lookup"><span data-stu-id="375eb-110">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="375eb-111">Это значительно увеличивает размер таблиц маршрутов, которые обслуживают маршрутизаторы в вашей сети.</span><span class="sxs-lookup"><span data-stu-id="375eb-111">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="375eb-112">Если вы планируете использовать только подмножество служб, предлагаемых через пиринг Майкрософт, размер таблиц маршрутизации можно уменьшить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="375eb-112">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="375eb-113">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="375eb-113">You can:</span></span>

- <span data-ttu-id="375eb-114">Отфильтровывать нежелательные префиксы путем применения фильтров маршрутов к сообществам BGP.</span><span class="sxs-lookup"><span data-stu-id="375eb-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="375eb-115">Это стандартная сетевая практика и обычно используется во многих сетях.</span><span class="sxs-lookup"><span data-stu-id="375eb-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="375eb-116">Определять фильтры маршрутов и применять их к каналу ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="375eb-116">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="375eb-117">Фильтр маршрутов — это новый ресурс, который позволяет выбрать список служб, которые вы собираетесь использовать через пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="375eb-117">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="375eb-118">Маршрутизаторы ExpressRoute отправляют только список префиксов, которые принадлежат службам, определяемым в фильтре маршрутов.</span><span class="sxs-lookup"><span data-stu-id="375eb-118">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <span data-ttu-id="375eb-119"><a name="about"></a>О фильтрах маршрута</span><span class="sxs-lookup"><span data-stu-id="375eb-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="375eb-120">При настроенном пиринге Майкрософт для канала ExpressRoute пограничные маршрутизаторы Майкрософт устанавливают пару сеансов BGP с пограничными маршрутизаторами (вашими или ваших поставщиков услуг подключения).</span><span class="sxs-lookup"><span data-stu-id="375eb-120">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="375eb-121">В вашей сети маршруты не объявляются.</span><span class="sxs-lookup"><span data-stu-id="375eb-121">No routes are advertised to your network.</span></span> <span data-ttu-id="375eb-122">Чтобы включить объявление маршрутов в своей сети, необходимо связать с ней фильтр маршрутов.</span><span class="sxs-lookup"><span data-stu-id="375eb-122">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="375eb-123">Фильтр маршрутов позволяет вам идентифицировать службы, которые можно использовать через пиринг Майкрософт по каналу ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="375eb-123">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="375eb-124">Это фактически белый список всех значений сообщества BGP.</span><span class="sxs-lookup"><span data-stu-id="375eb-124">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="375eb-125">После определения ресурса фильтра маршрута и его подключения к каналу ExpressRoute все префиксы, которые сопоставляются со значениями сообщества BGP, объявляются в сети.</span><span class="sxs-lookup"><span data-stu-id="375eb-125">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="375eb-126">Чтобы иметь возможность подключать фильтры маршрутов со службами Office 365, у вас должно быть разрешение на использование служб Office 365 через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="375eb-126">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="375eb-127">Если вы не авторизованы для использования служб Office 365 через ExpressRoute, произойдет сбой операции подключения фильтров маршрута.</span><span class="sxs-lookup"><span data-stu-id="375eb-127">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="375eb-128">Дополнительные сведения о процессе авторизации см. в статье [Azure ExpressRoute для Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="375eb-128">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="375eb-129">Подключение к службам Dynamics 365 не требует предварительного разрешения.</span><span class="sxs-lookup"><span data-stu-id="375eb-129">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="375eb-130">Пиринг Майкрософт для каналов ExpressRoute, которые были настроены до 1 августа 2017 г., позволяет объявлять все префиксы служб, даже если не настроены фильтры маршрутов.</span><span class="sxs-lookup"><span data-stu-id="375eb-130">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="375eb-131">Пиринг Майкрософт для каналов ExpressRoute, настроенных 1 августа 2017 г. или позднее, не будет объявлять префиксы, пока к каналу не будет присоединен фильтр маршрутов.</span><span class="sxs-lookup"><span data-stu-id="375eb-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span>
> 
> 

### <span data-ttu-id="375eb-132"><a name="workflow"></a>Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="375eb-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="375eb-133">Чтобы успешно подключиться к службам через пиринг Майкрософт, необходимо выполнить следующие действия по настройке:</span><span class="sxs-lookup"><span data-stu-id="375eb-133">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="375eb-134">Необходимо иметь активный канал ExpressRoute с подготовленным пирингом Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="375eb-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="375eb-135">Для выполнения этих задач можно использовать следующие инструкции:</span><span class="sxs-lookup"><span data-stu-id="375eb-135">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="375eb-136">[Создайте канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и включите его на стороне поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="375eb-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="375eb-137">Канал ExpressRoute должен находиться в подготовленном и включенном состоянии.</span><span class="sxs-lookup"><span data-stu-id="375eb-137">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="375eb-138">[Создайте пиринг Майкрософт](expressroute-howto-routing-portal-resource-manager.md), если вы управляете сеансом BGP напрямую</span><span class="sxs-lookup"><span data-stu-id="375eb-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="375eb-139">или если у вашего поставщика услуг подключения подготовлен пиринг Майкрософт для вашего канала.</span><span class="sxs-lookup"><span data-stu-id="375eb-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="375eb-140">Необходимо создать и настроить фильтр маршрутов.</span><span class="sxs-lookup"><span data-stu-id="375eb-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="375eb-141">Определите службы, которые вы будете использовать через пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="375eb-141">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="375eb-142">Определите список значений сообщества BGP, связанных со службами.</span><span class="sxs-lookup"><span data-stu-id="375eb-142">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="375eb-143">Создайте правило, чтобы разрешить список префиксов, соответствующих значениям сообщества BGP.</span><span class="sxs-lookup"><span data-stu-id="375eb-143">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="375eb-144">Фильтр маршрутов необходимо подключить к каналу ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="375eb-144">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="375eb-145">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="375eb-145">Before you begin</span></span>

<span data-ttu-id="375eb-146">Перед началом настройки убедитесь, что выполнены следующие условия:</span><span class="sxs-lookup"><span data-stu-id="375eb-146">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="375eb-147">Изучите [предварительные требования](expressroute-prerequisites.md) и [рабочие процессы](expressroute-workflows.md), прежде чем приступить к настройке.</span><span class="sxs-lookup"><span data-stu-id="375eb-147">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="375eb-148">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="375eb-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="375eb-149">Приступая к работе, [создайте канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md); он должен быть затем включен на стороне поставщика услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="375eb-149">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="375eb-150">Канал ExpressRoute должен находиться в подготовленном и включенном состоянии.</span><span class="sxs-lookup"><span data-stu-id="375eb-150">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="375eb-151">Необходимо иметь активный пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="375eb-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="375eb-152">Следуйте инструкциям в статье [Создание и изменение канала ExpressRoute с помощью PowerShell](expressroute-howto-routing-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="375eb-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="375eb-153"><a name="prefixes"></a>Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="375eb-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="375eb-154">Получение списка префиксов и значений сообщества BGP</span><span class="sxs-lookup"><span data-stu-id="375eb-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="375eb-155">1. Получение списка значений сообщества BGP</span><span class="sxs-lookup"><span data-stu-id="375eb-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="375eb-156">Значения BGP сообщества, связанные со службами, доступными через пиринг Майкрософт, приведены на странице [Требования к маршрутизации ExpressRoute](expressroute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="375eb-156">BGP community values associated with services accessible through Microsoft peering is available in the [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="375eb-157">2. Создание списка значений, которые можно использовать</span><span class="sxs-lookup"><span data-stu-id="375eb-157">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="375eb-158">Создайте список значений сообщества BGP, которые нужно использовать в фильтре маршрута.</span><span class="sxs-lookup"><span data-stu-id="375eb-158">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="375eb-159">Например, значение сообщества BGP для службы Dynamics 365 — 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="375eb-159">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="375eb-160"><a name="filter"></a>Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="375eb-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="375eb-161">Создание фильтра маршрута и правила фильтрации</span><span class="sxs-lookup"><span data-stu-id="375eb-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="375eb-162">Фильтр может иметь только одно правило, и оно должно иметь тип "Разрешить".</span><span class="sxs-lookup"><span data-stu-id="375eb-162">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="375eb-163">С этим правилом может быть связан список значений сообщества BGP.</span><span class="sxs-lookup"><span data-stu-id="375eb-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="375eb-164">1. Создание фильтра маршрута</span><span class="sxs-lookup"><span data-stu-id="375eb-164">1. Create a route filter</span></span>
<span data-ttu-id="375eb-165">Чтобы создать фильтр маршрута, необходимо выбрать команду создания ресурса.</span><span class="sxs-lookup"><span data-stu-id="375eb-165">You can create a route filter by selecting the option to create a new resource.</span></span> <span data-ttu-id="375eb-166">Выберите **Создать** > **Сети** > **RouteFilter**, как показано на рисунке ниже:</span><span class="sxs-lookup"><span data-stu-id="375eb-166">Click **New** > **Networking** > **RouteFilter**, as shown in the following image:</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="375eb-168">Фильтр маршрута необходимо разместить в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="375eb-168">You must place the route filter in a resource group.</span></span> 

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="375eb-170">2. Создание правила фильтрации</span><span class="sxs-lookup"><span data-stu-id="375eb-170">2. Create a filter rule</span></span>

<span data-ttu-id="375eb-171">Можно добавлять и обновлять правила, выбрав вкладку "Управление правилами фильтра маршрута".</span><span class="sxs-lookup"><span data-stu-id="375eb-171">You can add and update rules by selecting the manage rule tab for your route filter.</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="375eb-173">Можно выбрать службы, к которым необходимо подключиться из раскрывающегося списка, и сохранить правило после завершения.</span><span class="sxs-lookup"><span data-stu-id="375eb-173">You can select the services you want to connect to from the drop down list and save the rule when done.</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="375eb-175"><a name="attach"></a>Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="375eb-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="375eb-176">Подключения фильтра маршрута к каналу ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="375eb-176">Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="375eb-177">Фильтр маршрутов можно вложить в схему, нажав кнопку "Добавить схемы" и выбрав схему ExpressRoute из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="375eb-177">You can attach the route filter to a circuit by selecting the "add Circuit" button and selecting the ExpressRoute circuit from the drop down list.</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="375eb-179"><a name="getproperties"></a>Получение свойств фильтра маршрута</span><span class="sxs-lookup"><span data-stu-id="375eb-179"><a name="getproperties"></a>To get the properties of a route filter</span></span>

<span data-ttu-id="375eb-180">Открыв ресурс на портале, можно просмотреть свойства фильтра маршрута.</span><span class="sxs-lookup"><span data-stu-id="375eb-180">You can view properties of a route filter when you open the resource in the portal.</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="375eb-182"><a name="updateproperties"></a>Обновление свойств фильтра маршрутов</span><span class="sxs-lookup"><span data-stu-id="375eb-182"><a name="updateproperties"></a>To update the properties of a route filter</span></span>

<span data-ttu-id="375eb-183">Нажав кнопку "Управление правилом", можно обновить список значений сообщества BGP, присоединенного к схеме.</span><span class="sxs-lookup"><span data-stu-id="375eb-183">You can update the list of BGP community values attached to a circuit by selecting the "Manage rule" button.</span></span>


![Создание фильтра маршрута](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="375eb-186"><a name="detach"></a>Отсоединение фильтра маршрутов от канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="375eb-186"><a name="detach"></a>To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="375eb-187">Чтобы отсоединить канал от фильтра маршрутов, щелкните канал правой кнопкой мыши и выберите "Отменить связь".</span><span class="sxs-lookup"><span data-stu-id="375eb-187">To detach a circuit from the route filter, right click on the circuit and click on "disassociate".</span></span>

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="375eb-189"><a name="delete"></a>Удаление фильтра маршрутов</span><span class="sxs-lookup"><span data-stu-id="375eb-189"><a name="delete"></a>To delete a route filter</span></span>

<span data-ttu-id="375eb-190">Фильтр маршрута можно удалить, нажав кнопку "Удалить".</span><span class="sxs-lookup"><span data-stu-id="375eb-190">You can delete a route filter by selecting the delete button.</span></span> 

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="375eb-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="375eb-192">Next steps</span></span>

<span data-ttu-id="375eb-193">Дополнительные сведения об ExpressRoute см. в статье [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="375eb-193">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>