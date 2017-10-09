---
title: "Настройка фильтров маршрутов для пиринга Azure ExpressRoute Microsoft с помощью PowerShell | Документация Майкрософт"
description: "В этой статье описывается, как фильтры tooconfigure маршрута для Пиринга Майкрософт с помощью PowerShell"
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="cfb45-103">Настройка фильтров маршрутов для пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="cfb45-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="cfb45-104">Фильтры маршрутов являются способом tooconsume подмножество поддерживаемых услуг через пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cfb45-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="cfb45-105">Hello шаги, приведенные в этой статье справки можно настраивать и управлять фильтры маршрутов для каналов ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="cfb45-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="cfb45-106">Службы Dynamics 365 и службам Office 365, такие как Exchange Online, SharePoint Online и Скайп для бизнеса, доступны через пиринг Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="cfb45-107">При настройке пиринг Майкрософт в канал ExpressRoute, через сеансов BGP hello, установленных объявления все префиксы toothese связанных служб.</span><span class="sxs-lookup"><span data-stu-id="cfb45-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="cfb45-108">Значение сообщества BGP является hello вложенного tooevery префикс tooidentify службы, предлагаемые hello префикс.</span><span class="sxs-lookup"><span data-stu-id="cfb45-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="cfb45-109">Список значений сообщества BGP hello и hello служб, они сопоставляются. в разделе [BGP сообщества](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="cfb45-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="cfb45-110">Если необходимо использовать службы связи tooall, большое число префиксов разглашаемые BGP.</span><span class="sxs-lookup"><span data-stu-id="cfb45-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="cfb45-111">Это значительно увеличивает размер hello таблиц маршрутов hello обслуживается маршрутизаторов в сети.</span><span class="sxs-lookup"><span data-stu-id="cfb45-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="cfb45-112">Если планируется tooconsume только подмножество служб, предлагаемым через пиринг Майкрософт, можно уменьшить размер hello таблиц маршрутизации двумя способами.</span><span class="sxs-lookup"><span data-stu-id="cfb45-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="cfb45-113">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="cfb45-113">You can:</span></span>

- <span data-ttu-id="cfb45-114">Отфильтровывать нежелательные префиксы путем применения фильтров маршрутов к сообществам BGP.</span><span class="sxs-lookup"><span data-stu-id="cfb45-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="cfb45-115">Это стандартная сетевая практика и обычно используется во многих сетях.</span><span class="sxs-lookup"><span data-stu-id="cfb45-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="cfb45-116">Определение фильтров маршрута и применить их tooyour канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="cfb45-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="cfb45-117">Фильтр — новый ресурс, что позволяет выбрать hello список служб, которые планирование tooconsume через пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cfb45-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="cfb45-118">ExpressRoute они передают лишь hello список префиксов, которые принадлежат toohello службы, определенные в фильтре hello маршрута.</span><span class="sxs-lookup"><span data-stu-id="cfb45-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="cfb45-119"><a name="about"></a>О фильтрах маршрута</span><span class="sxs-lookup"><span data-stu-id="cfb45-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="cfb45-120">Когда пиринг Майкрософт настроена на ваш канал ExpressRoute, периметрическими маршрутизаторами Microsoft hello установить паре сеансов BGP с маршрутизаторами edge hello (вашим или поставщика услуг подключения).</span><span class="sxs-lookup"><span data-stu-id="cfb45-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="cfb45-121">Маршруты, объявленные tooyour сети.</span><span class="sxs-lookup"><span data-stu-id="cfb45-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="cfb45-122">tooenable объявления tooyour маршруте, необходимо связать фильтр маршрутов.</span><span class="sxs-lookup"><span data-stu-id="cfb45-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="cfb45-123">Фильтр позволяет выявить службы будут tooconsume через пиринг Майкрософт канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="cfb45-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="cfb45-124">Это по сути белый список значений всех hello BGP сообщества.</span><span class="sxs-lookup"><span data-stu-id="cfb45-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="cfb45-125">После определен и присоединенного tooan канал ExpressRoute ресурса фильтров маршрута, все префиксы, сопоставленные toohello BGP сообщества значения являются объявленной tooyour сети.</span><span class="sxs-lookup"><span data-stu-id="cfb45-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="cfb45-126">фильтры маршрутов может tooattach toobe со службами Office 365 на них, необходимо иметь авторизации служб Office 365 tooconsume через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="cfb45-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="cfb45-127">При отсутствии службы авторизованным tooconsume Office 365 с помощью ExpressRoute, фильтры маршрутов tooattach hello операция завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="cfb45-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="cfb45-128">Дополнительные сведения о процессе авторизации hello см. в разделе [ExpressRoute Azure для Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="cfb45-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="cfb45-129">Службы 365 tooDynamics связи не требуется никакой предыдущих авторизации.</span><span class="sxs-lookup"><span data-stu-id="cfb45-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cfb45-130">Microsoft пиринг ExpressRoute каналов, которые были настроены предыдущих tooAugust 1, 2017 г. будет иметь все службы префиксов, объявленных через пиринг Майкрософт, даже если не определены фильтры маршрутов.</span><span class="sxs-lookup"><span data-stu-id="cfb45-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="cfb45-131">Пиринг каналы ExpressRoute, настроенных в течение или после 1 августа 2017 г. Корпорация Майкрософт не будет иметь префиксы объявленных пока фильтр не будет подключено toohello канала.</span><span class="sxs-lookup"><span data-stu-id="cfb45-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="cfb45-132"><a name="workflow"></a>Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="cfb45-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="cfb45-133">возможности toosuccessfully toobe подключение tooservices через пиринг Майкрософт, необходимо выполнить следующие действия по настройке hello:</span><span class="sxs-lookup"><span data-stu-id="cfb45-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="cfb45-134">Необходимо иметь активный канал ExpressRoute с подготовленным пирингом Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cfb45-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="cfb45-135">Эти задачи можно использовать следующие инструкции tooaccomplish hello:</span><span class="sxs-lookup"><span data-stu-id="cfb45-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="cfb45-136">[Создайте канал ExpressRoute](expressroute-howto-circuit-arm.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="cfb45-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="cfb45-137">Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен.</span><span class="sxs-lookup"><span data-stu-id="cfb45-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="cfb45-138">[Создайте пиринг Майкрософт](expressroute-circuit-peerings.md) при управлении hello непосредственно в сеансе BGP.</span><span class="sxs-lookup"><span data-stu-id="cfb45-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="cfb45-139">или если у вашего поставщика услуг подключения подготовлен пиринг Майкрософт для вашего канала.</span><span class="sxs-lookup"><span data-stu-id="cfb45-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="cfb45-140">Необходимо создать и настроить фильтр маршрутов.</span><span class="sxs-lookup"><span data-stu-id="cfb45-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="cfb45-141">Определите hello сервисы tooconsume через пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="cfb45-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="cfb45-142">Определить hello список значений BGP сообщества, связанные со службами hello</span><span class="sxs-lookup"><span data-stu-id="cfb45-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="cfb45-143">Создать правило tooallow hello префикс список сопоставления hello значения BGP сообщества</span><span class="sxs-lookup"><span data-stu-id="cfb45-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="cfb45-144">Необходимо добавить канал ExpressRoute toohello фильтра маршрута hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cfb45-145">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="cfb45-145">Before you begin</span></span>

<span data-ttu-id="cfb45-146">Перед началом настройки убедитесь, что соблюдены следующие условия hello:</span><span class="sxs-lookup"><span data-stu-id="cfb45-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="cfb45-147">Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="cfb45-147">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="cfb45-148">Дополнительные сведения см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="cfb45-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="cfb45-149">Загрузка последней версии hello из коллекции PowerShell hello, а не с помощью установщика hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-149">Download hello latest version from hello PowerShell Gallery, rather than using hello Installer.</span></span> <span data-ttu-id="cfb45-150">Hello установщика в настоящее время не поддерживает командлеты необходимые hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-150">hello Installer currently does not support hello required cmdlets.</span></span>
  > 

 - <span data-ttu-id="cfb45-151">Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="cfb45-151">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="cfb45-152">Вам потребуется активный канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="cfb45-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="cfb45-153">Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="cfb45-153">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="cfb45-154">Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен.</span><span class="sxs-lookup"><span data-stu-id="cfb45-154">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="cfb45-155">Необходимо иметь активный пиринг Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cfb45-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="cfb45-156">Следуйте инструкциям в статье [Создание и изменение канала ExpressRoute с помощью PowerShell](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="cfb45-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="cfb45-157">Войдите в tooyour учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="cfb45-157">Log in tooyour Azure account</span></span>

<span data-ttu-id="cfb45-158">Перед началом этой конфигурации, необходимо войти в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="cfb45-158">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="cfb45-159">Hello командлет запросит hello учетные данные входа для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="cfb45-159">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="cfb45-160">После входа в систему, он загружает параметры учетной записи, таким образом, они будут доступны tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cfb45-160">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="cfb45-161">Откройте консоль PowerShell с повышенными привилегиями и подключите tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="cfb45-161">Open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="cfb45-162">Используйте следующий пример toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-162">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="cfb45-163">Если у вас несколько подписок Azure, проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-163">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="cfb45-164">Укажите требуемый toouse подписки hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-164">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="cfb45-165"><a name="prefixes"></a>Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="cfb45-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="cfb45-166">Получение списка префиксов и значений сообщества BGP</span><span class="sxs-lookup"><span data-stu-id="cfb45-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="cfb45-167">1. Получение списка значений сообщества BGP</span><span class="sxs-lookup"><span data-stu-id="cfb45-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="cfb45-168">Используйте следующий командлет tooget hello список значений BGP сообщества, связанные со службами, доступными через пиринг Майкрософт hello и hello список префиксов, связанные с ними:</span><span class="sxs-lookup"><span data-stu-id="cfb45-168">Use hello following cmdlet tooget hello list of BGP community values associated with services accessible through Microsoft peering, and hello list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="cfb45-169">2. Создайте список значений hello, которые должны toouse</span><span class="sxs-lookup"><span data-stu-id="cfb45-169">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="cfb45-170">Составьте список нужные значения сообщества BGP toouse в фильтре hello маршрута.</span><span class="sxs-lookup"><span data-stu-id="cfb45-170">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="cfb45-171">Например значение сообщества BGP для службы Dynamics 365 hello — 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="cfb45-171">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="cfb45-172"><a name="filter"></a>Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="cfb45-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="cfb45-173">Создание фильтра маршрута и правила фильтрации</span><span class="sxs-lookup"><span data-stu-id="cfb45-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="cfb45-174">Фильтр может иметь только одно правило и hello правило должно иметь тип «Разрешить».</span><span class="sxs-lookup"><span data-stu-id="cfb45-174">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="cfb45-175">С этим правилом может быть связан список значений сообщества BGP.</span><span class="sxs-lookup"><span data-stu-id="cfb45-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="cfb45-176">1. Создание фильтра маршрута</span><span class="sxs-lookup"><span data-stu-id="cfb45-176">1. Create a route filter</span></span>

<span data-ttu-id="cfb45-177">Сначала создайте фильтр маршрутов hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-177">First, create hello route filter.</span></span> <span data-ttu-id="cfb45-178">Команда Hello «New-AzureRmRouteFilter» только создает ресурс фильтра маршрута.</span><span class="sxs-lookup"><span data-stu-id="cfb45-178">hello command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="cfb45-179">После создания ресурса hello, необходимо создать правило и присоединить его объект filter toohello маршрута.</span><span class="sxs-lookup"><span data-stu-id="cfb45-179">After you create hello resource, you must then create a rule and attach it toohello route filter object.</span></span> <span data-ttu-id="cfb45-180">Запустите следующие команды toocreate hello ресурс фильтра маршрута:</span><span class="sxs-lookup"><span data-stu-id="cfb45-180">Run hello following command toocreate a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="cfb45-181">2. Создание правила фильтрации</span><span class="sxs-lookup"><span data-stu-id="cfb45-181">2. Create a filter rule</span></span>

<span data-ttu-id="cfb45-182">Можно указать набор сообщества BGP как список с разделителями запятыми, как показано в примере hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-182">You can specify a set of BGP communities as a comma-separated list, as shown in hello example.</span></span> <span data-ttu-id="cfb45-183">Выполните следующие команды toocreate hello новое правило.</span><span class="sxs-lookup"><span data-stu-id="cfb45-183">Run hello following command toocreate a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a><span data-ttu-id="cfb45-184">3. Добавить фильтр маршрутов toohello правило hello</span><span class="sxs-lookup"><span data-stu-id="cfb45-184">3. Add hello rule toohello route filter</span></span>

<span data-ttu-id="cfb45-185">Следующая команда tooadd hello правило toohello маршрута фильтр выполнения hello:</span><span class="sxs-lookup"><span data-stu-id="cfb45-185">Run hello following command tooadd hello filter rule toohello route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="cfb45-186"><a name="attach"></a>Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="cfb45-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="cfb45-187">Присоединение канал ExpressRoute tooan фильтра маршрута hello</span><span class="sxs-lookup"><span data-stu-id="cfb45-187">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="cfb45-188">Выполните следующие команды tooattach hello маршрута фильтра toohello канал ExpressRoute, при условии, что у вас есть только пиринг Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-188">Run hello following command tooattach hello route filter toohello ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="cfb45-189"><a name="getproperties"></a>свойства hello tooget фильтра маршрута</span><span class="sxs-lookup"><span data-stu-id="cfb45-189"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="cfb45-190">свойства hello tooget фильтр маршрутов hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="cfb45-190">tooget hello properties of a route filter, use hello following steps:</span></span>

1. <span data-ttu-id="cfb45-191">Следующая команда tooget hello маршрута фильтр ресурсов выполнения hello:</span><span class="sxs-lookup"><span data-stu-id="cfb45-191">Run hello following command tooget hello route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="cfb45-192">Получите правила фильтрации hello маршрута для ресурса hello фильтра маршрутов, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="cfb45-192">Get hello route filter rules for hello route-filter resource by running hello following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="cfb45-193"><a name="updateproperties"></a>свойства hello tooupdate фильтра маршрута</span><span class="sxs-lookup"><span data-stu-id="cfb45-193"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="cfb45-194">Если фильтр маршрутов hello уже присоединен tooa цепи, список сообщества BGP toohello обновления автоматически распространяет изменения объявления соответствующий префикс при помощи сеансов BGP hello установлено.</span><span class="sxs-lookup"><span data-stu-id="cfb45-194">If hello route filter is already attached tooa circuit, updates toohello BGP community list automatically propagates appropriate prefix advertisement changes through hello established BGP sessions.</span></span> <span data-ttu-id="cfb45-195">Можно обновить список сообщества BGP hello фильтра маршрута с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cfb45-195">You can update hello BGP community list of your route filter using hello following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="cfb45-196"><a name="detach"></a>toodetach фильтр маршрутов из канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="cfb45-196"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="cfb45-197">Как только фильтр отсоединяется от hello канал ExpressRoute, отсутствуют префиксы объявления через сеанс BGP hello.</span><span class="sxs-lookup"><span data-stu-id="cfb45-197">Once a route filter is detached from hello ExpressRoute circuit, no prefixes are advertised through hello BGP session.</span></span> <span data-ttu-id="cfb45-198">Можно отсоединить фильтр маршрутов из канала ExpressRoute с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cfb45-198">You can detach a route filter from an ExpressRoute circuit using hello following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="cfb45-199"><a name="delete"></a>toodelete фильтр маршрутов</span><span class="sxs-lookup"><span data-stu-id="cfb45-199"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="cfb45-200">Можно только удалить фильтр маршрута, если он не присоединен tooany канала.</span><span class="sxs-lookup"><span data-stu-id="cfb45-200">You can only delete a route filter if it is not attached tooany circuit.</span></span> <span data-ttu-id="cfb45-201">Убедитесь, этот фильтр маршрута hello не присоединен tooany схемы перед выполнением toodelete его.</span><span class="sxs-lookup"><span data-stu-id="cfb45-201">Ensure that hello route filter is not attached tooany circuit before attempting toodelete it.</span></span> <span data-ttu-id="cfb45-202">Можно удалить фильтр с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cfb45-202">You can delete a route filter using hello following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="cfb45-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cfb45-203">Next steps</span></span>

<span data-ttu-id="cfb45-204">Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="cfb45-204">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
