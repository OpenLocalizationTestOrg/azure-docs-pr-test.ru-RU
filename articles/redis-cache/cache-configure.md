---
title: "aaaHow tooconfigure кэша Redis для Azure | Документы Microsoft"
description: "Обзор конфигурации Redis по умолчанию hello для кэша Redis для Azure и узнайте, как tooconfigure Azure Redis кэш экземпляров"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a><span data-ttu-id="1f113-103">Как tooconfigure Redis для Azure кэша</span><span class="sxs-lookup"><span data-stu-id="1f113-103">How tooconfigure Azure Redis Cache</span></span>
<span data-ttu-id="1f113-104">В этом разделе описывается, как tooreview и обновление hello конфигурации для экземпляров кэша Redis для Azure и конфигурация сервера Redis по умолчанию hello обложки для экземпляров кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="1f113-104">This topic describes how tooreview and update hello configuration for your Azure Redis Cache instances, and covers hello default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="1f113-105">Дополнительные сведения о настройке и использовании функции кэша premium см. в разделе [как сохраняемости tooconfigure](cache-how-to-premium-persistence.md), [как кластеризация tooconfigure](cache-how-to-premium-clustering.md), и [как поддерживают tooconfigure виртуальной сети ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-105">For more information on configuring and using premium cache features, see [How tooconfigure persistence](cache-how-to-premium-persistence.md), [How tooconfigure clustering](cache-how-to-premium-clustering.md), and [How tooconfigure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="1f113-106">Настройка параметров кэша Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="1f113-107">Параметры кэша Redis для Azure просмотреть и настроить на hello **кэша Redis** колонке с помощью hello **ресурсов меню**.</span><span class="sxs-lookup"><span data-stu-id="1f113-107">Azure Redis Cache settings are viewed and configured on hello **Redis Cache** blade using hello **Resource Menu**.</span></span>

![Параметры кэша Redis](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="1f113-109">Можно просмотреть и настроить следующие параметры с помощью hello hello **ресурсов меню**.</span><span class="sxs-lookup"><span data-stu-id="1f113-109">You can view and configure hello following settings using hello **Resource Menu**.</span></span>

* [<span data-ttu-id="1f113-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="1f113-110">Overview</span></span>](#overview)
* [<span data-ttu-id="1f113-111">Журнал действий</span><span class="sxs-lookup"><span data-stu-id="1f113-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="1f113-112">Управление доступом (IAM)</span><span class="sxs-lookup"><span data-stu-id="1f113-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="1f113-113">Теги</span><span class="sxs-lookup"><span data-stu-id="1f113-113">Tags</span></span>](#tags)
* [<span data-ttu-id="1f113-114">Диагностика и решение проблем</span><span class="sxs-lookup"><span data-stu-id="1f113-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="1f113-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="1f113-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="1f113-116">Ключи доступа</span><span class="sxs-lookup"><span data-stu-id="1f113-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="1f113-117">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="1f113-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="1f113-118">Помощник по кэшу Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="1f113-119">Масштабирование</span><span class="sxs-lookup"><span data-stu-id="1f113-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="1f113-120">Размер кластера Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="1f113-121">Сохраняемость данных Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="1f113-122">Планирование обновлений</span><span class="sxs-lookup"><span data-stu-id="1f113-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="1f113-123">Георепликация</span><span class="sxs-lookup"><span data-stu-id="1f113-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="1f113-124">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="1f113-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="1f113-125">Брандмауэр</span><span class="sxs-lookup"><span data-stu-id="1f113-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="1f113-126">Свойства</span><span class="sxs-lookup"><span data-stu-id="1f113-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="1f113-127">Блокировки</span><span class="sxs-lookup"><span data-stu-id="1f113-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="1f113-128">Сценарий автоматизации</span><span class="sxs-lookup"><span data-stu-id="1f113-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="1f113-129">Администрирование</span><span class="sxs-lookup"><span data-stu-id="1f113-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="1f113-130">Импорт данных</span><span class="sxs-lookup"><span data-stu-id="1f113-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="1f113-131">Экспорт данных</span><span class="sxs-lookup"><span data-stu-id="1f113-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="1f113-132">Reboot</span><span class="sxs-lookup"><span data-stu-id="1f113-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="1f113-133">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="1f113-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="1f113-134">Метрики Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="1f113-135">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="1f113-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="1f113-136">Диагностика</span><span class="sxs-lookup"><span data-stu-id="1f113-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="1f113-137">Настройки поддержки и устранения неполадок</span><span class="sxs-lookup"><span data-stu-id="1f113-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="1f113-138">Работоспособность ресурса</span><span class="sxs-lookup"><span data-stu-id="1f113-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="1f113-139">Новый запрос в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="1f113-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="1f113-140">Обзор</span><span class="sxs-lookup"><span data-stu-id="1f113-140">Overview</span></span>

<span data-ttu-id="1f113-141">В разделе **Обзор** содержатся основные сведения о кэше, такие как имя, порты, ценовая категория, и выбранные метрики кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="1f113-142">Журнал действий</span><span class="sxs-lookup"><span data-stu-id="1f113-142">Activity log</span></span>

<span data-ttu-id="1f113-143">Нажмите кнопку **журнал действий** tooview действия, выполняемые с вашего кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-143">Click **Activity log** tooview actions performed on your cache.</span></span> <span data-ttu-id="1f113-144">Можно также использовать tooexpand фильтрации этого представления tooinclude другие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1f113-144">You can also use filtering tooexpand this view tooinclude other resources.</span></span> <span data-ttu-id="1f113-145">Дополнительные сведения об использовании журналов аудита см. в статье [Просмотр журналов действий для аудита действий с ресурсами](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="1f113-146">Дополнительные сведения о мониторинге событий кэша Redis для Azure см. в разделе [Операции и оповещения](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="1f113-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="1f113-147">Управление доступом (IAM)</span><span class="sxs-lookup"><span data-stu-id="1f113-147">Access control (IAM)</span></span>

<span data-ttu-id="1f113-148">Hello **(IAM) управления доступом к** раздел предоставляет поддержку для управления доступом на основе ролей (RBAC) в hello Azure toohelp портала организации соответствуют свои требования к управлению доступом просто и точно выполнять.</span><span class="sxs-lookup"><span data-stu-id="1f113-148">hello **Access control (IAM)** section provides support for role-based access control (RBAC) in hello Azure portal toohelp organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="1f113-149">Дополнительные сведения см. в разделе [управление доступом на основе ролей в hello портал Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-149">For more information, see [Role-based access control in hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="1f113-150">Теги</span><span class="sxs-lookup"><span data-stu-id="1f113-150">Tags</span></span>

<span data-ttu-id="1f113-151">Hello **теги** раздел помогает организовать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1f113-151">hello **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="1f113-152">Дополнительные сведения см. в разделе [использование теги tooorganize ресурсам Azure](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-152">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="1f113-153">Диагностика и решение проблем</span><span class="sxs-lookup"><span data-stu-id="1f113-153">Diagnose and solve problems</span></span>

<span data-ttu-id="1f113-154">Нажмите кнопку **диагностики и устранения неполадок** toobe предоставлены общие проблемы и стратегии по их устранению.</span><span class="sxs-lookup"><span data-stu-id="1f113-154">Click **Diagnose and solve problems** toobe provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="1f113-155">данных</span><span class="sxs-lookup"><span data-stu-id="1f113-155">Settings</span></span>
<span data-ttu-id="1f113-156">Hello **параметры** раздел позволяет вам tooaccess и настройте следующие параметры кэша hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-156">hello **Settings** section allows you tooaccess and configure hello following settings for your cache.</span></span>

* [<span data-ttu-id="1f113-157">Ключи доступа</span><span class="sxs-lookup"><span data-stu-id="1f113-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="1f113-158">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="1f113-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="1f113-159">Помощник по кэшу Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="1f113-160">Масштабирование</span><span class="sxs-lookup"><span data-stu-id="1f113-160">Scale</span></span>](#scale)
* [<span data-ttu-id="1f113-161">Размер кластера Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="1f113-162">Сохраняемость данных Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="1f113-163">Планирование обновлений</span><span class="sxs-lookup"><span data-stu-id="1f113-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="1f113-164">Георепликация</span><span class="sxs-lookup"><span data-stu-id="1f113-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="1f113-165">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="1f113-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="1f113-166">Брандмауэр</span><span class="sxs-lookup"><span data-stu-id="1f113-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="1f113-167">Свойства</span><span class="sxs-lookup"><span data-stu-id="1f113-167">Properties</span></span>](#properties)
* [<span data-ttu-id="1f113-168">Блокировки</span><span class="sxs-lookup"><span data-stu-id="1f113-168">Locks</span></span>](#locks)
* [<span data-ttu-id="1f113-169">Сценарий автоматизации</span><span class="sxs-lookup"><span data-stu-id="1f113-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="1f113-170">Ключи доступа</span><span class="sxs-lookup"><span data-stu-id="1f113-170">Access keys</span></span>
<span data-ttu-id="1f113-171">Нажмите кнопку **ключи доступа** tooview или повторно создайте доступ hello ключи для вашего кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-171">Click **Access keys** tooview or regenerate hello access keys for your cache.</span></span> <span data-ttu-id="1f113-172">Эти ключи используются hello клиенты, подключающиеся tooyour кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-172">These keys are used by hello clients connecting tooyour cache.</span></span>

![Ключи доступа кэша Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="1f113-174">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="1f113-174">Advanced settings</span></span>
<span data-ttu-id="1f113-175">Hello следующие параметры настраиваются на hello **Дополнительные параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="1f113-175">hello following settings are configured on hello **Advanced settings** blade.</span></span>

* [<span data-ttu-id="1f113-176">Порты доступа</span><span class="sxs-lookup"><span data-stu-id="1f113-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="1f113-177">Политики памяти</span><span class="sxs-lookup"><span data-stu-id="1f113-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="1f113-178">Уведомления пространства ключей (дополнительные параметры)</span><span class="sxs-lookup"><span data-stu-id="1f113-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="1f113-179">Порты доступа</span><span class="sxs-lookup"><span data-stu-id="1f113-179">Access Ports</span></span>
<span data-ttu-id="1f113-180">Для новых кэшей без SSL порт по умолчанию отключен.</span><span class="sxs-lookup"><span data-stu-id="1f113-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="1f113-181">tooenable hello не SSL порт, щелкните **нет** для **разрешить доступ только через SSL** на hello **Дополнительные параметры** колонку и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1f113-181">tooenable hello non-SSL port, click **No** for **Allow access only via SSL** on hello **Advanced settings** blade and then click **Save**.</span></span>

![Порты доступа кэша Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="1f113-183">Политики памяти</span><span class="sxs-lookup"><span data-stu-id="1f113-183">Memory policies</span></span>
<span data-ttu-id="1f113-184">Hello **политику Maxmemory**, **зарезервировано maxmemory**, и **зарезервировано maxfragmentationmemory** параметры на hello **Дополнительные параметры**колонку настройки политик памяти hello для кэша hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-184">hello **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on hello **Advanced settings** blade configure hello memory policies for hello cache.</span></span>

![Политика максимальной памяти кэша Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="1f113-186">**Политика максимальной памяти** настраивает политику кэша hello вытеснения hello и позволяет toochoose из hello следующие политики вытеснения:</span><span class="sxs-lookup"><span data-stu-id="1f113-186">**Maxmemory policy** configures hello eviction policy for hello cache and allows you toochoose from hello following eviction policies:</span></span>

* <span data-ttu-id="1f113-187">`volatile-lru`-Это по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-187">`volatile-lru` - this is hello default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="1f113-188">Дополнительные сведения о политиках `maxmemory` см. в разделе [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies) (Политики вытеснения) на сайте Redis.</span><span class="sxs-lookup"><span data-stu-id="1f113-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="1f113-189">Hello **maxmemory зарезервировано** параметр настраивает hello объем памяти в Мегабайтах, который зарезервирован для операции не из кэша, такие как репликации во время отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="1f113-189">hello **maxmemory-reserved** setting configures hello amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="1f113-190">Установка этого значения можно toohave более согласованной работы сервера Redis при зависит от нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1f113-190">Setting this value allows you toohave a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="1f113-191">Это значение должно быть выше при рабочих нагрузках с преобладанием записи.</span><span class="sxs-lookup"><span data-stu-id="1f113-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="1f113-192">При резервировании памяти для таких операций она недоступна для хранения кэшированных данных.</span><span class="sxs-lookup"><span data-stu-id="1f113-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="1f113-193">Hello **maxfragmentationmemory зарезервировано** параметр настраивает hello объем памяти в Мегабайтах, который является зарезервированным tooaccommodate для фрагментации памяти.</span><span class="sxs-lookup"><span data-stu-id="1f113-193">hello **maxfragmentationmemory-reserved** setting configures hello amount of memory in MB that is reserved tooaccommodate for memory fragmentation.</span></span> <span data-ttu-id="1f113-194">Установка этого значения можно toohave более согласованной работы сервера Redis при hello кэш не заполнится или закрыть соотношение фрагментации toofull и hello также высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="1f113-194">Setting this value allows you toohave a more consistent Redis server experience when hello cache is full or close toofull and hello fragmentation ratio is also high.</span></span> <span data-ttu-id="1f113-195">При резервировании памяти для таких операций она недоступна для хранения кэшированных данных.</span><span class="sxs-lookup"><span data-stu-id="1f113-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="1f113-196">Единственное tooconsider при выборе нового значения резервирование памяти (**зарезервировано maxmemory** или **maxfragmentationmemory зарезервировано**) является, как это изменение может повлиять на кэш, который уже выполняется с большие объемы данных в ней.</span><span class="sxs-lookup"><span data-stu-id="1f113-196">One thing tooconsider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="1f113-197">Например если кэш 53 ГБ с 49 ГБ данных, а затем измените значение too8 hello резервирования ГБ, это будет удалена hello max доступной памяти для системы hello вниз too45 ГБ.</span><span class="sxs-lookup"><span data-stu-id="1f113-197">For instance, if you have a 53 GB cache with 49 GB of data, then change hello reservation value too8 GB, this will drop hello max available memory for hello system down too45 GB.</span></span> <span data-ttu-id="1f113-198">Если ваши текущие `used_memory` или `used_memory_rss` значения выше, чем новый предел hello 45 ГБ, а затем hello система будет иметь tooevict данных, пока оба `used_memory` и `used_memory_rss` ниже 45 ГБ.</span><span class="sxs-lookup"><span data-stu-id="1f113-198">If either your current `used_memory` or your `used_memory_rss` values are higher than hello new limit of 45 GB, then hello system will have tooevict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="1f113-199">Вытеснение может увеличить нагрузку на сервер и фрагментацию памяти.</span><span class="sxs-lookup"><span data-stu-id="1f113-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="1f113-200">Дополнительные сведения о доступных метриках кэша, таких как `used_memory` и `used_memory_rss`, см. в разделе [Доступные метрики и интервалы отчетности](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="1f113-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f113-201">Hello **зарезервировано maxmemory** и **maxfragmentationmemory зарезервировано** параметры доступны только для Standard и Premium кэширует.</span><span class="sxs-lookup"><span data-stu-id="1f113-201">hello **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="1f113-202">Уведомления пространства ключей (дополнительные параметры)</span><span class="sxs-lookup"><span data-stu-id="1f113-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="1f113-203">Redis на hello настраиваются уведомления keyspace **Дополнительные параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="1f113-203">Redis keyspace notifications are configured on hello **Advanced settings** blade.</span></span> <span data-ttu-id="1f113-204">Уведомления Keyspace позволяют клиентам tooreceive уведомления при возникновении определенных событий.</span><span class="sxs-lookup"><span data-stu-id="1f113-204">Keyspace notifications allow clients tooreceive notifications when certain events occur.</span></span>

![Дополнительные параметры кэша Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="1f113-206">Пространство ключей уведомлений и hello **уведомления keyspace событий** параметра доступны только для кэша Standard и Premium.</span><span class="sxs-lookup"><span data-stu-id="1f113-206">Keyspace notifications and hello **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="1f113-207">Дополнительные сведения см. в статье [Redis Keyspace Notifications](http://redis.io/topics/notifications) (Уведомления пространства ключей Redis).</span><span class="sxs-lookup"><span data-stu-id="1f113-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="1f113-208">Пример кода, в разделе hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) файла в hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) образца.</span><span class="sxs-lookup"><span data-stu-id="1f113-208">For sample code, see hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="1f113-209">Помощник по кэшу Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-209">Redis Cache Advisor</span></span>
<span data-ttu-id="1f113-210">Hello **Advisor кэша Redis** колонке приводятся рекомендации для кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-210">hello **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="1f113-211">Во время обычной работы не отображается никаких рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="1f113-211">During normal operations, no recommendations are displayed.</span></span> 

![Рекомендации](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="1f113-213">При любых условиях происходят во время операций hello вашего кэша, например использовании большого объема памяти, пропускной способности сети или нагрузки на сервер, на hello отображаются оповещение **кэша Redis** колонку.</span><span class="sxs-lookup"><span data-stu-id="1f113-213">If any conditions occur during hello operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on hello **Redis Cache** blade.</span></span>

![Рекомендации](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="1f113-215">Дополнительные сведения можно найти на hello **рекомендации** колонку.</span><span class="sxs-lookup"><span data-stu-id="1f113-215">Further information can be found on hello **Recommendations** blade.</span></span>

![Рекомендации](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="1f113-217">Вы можете отслеживать эти метрики на hello [диаграммы мониторинга](cache-how-to-monitor.md#monitoring-charts) и [диаграммы использования](cache-how-to-monitor.md#usage-charts) разделы hello **кэша Redis** колонку.</span><span class="sxs-lookup"><span data-stu-id="1f113-217">You can monitor these metrics on hello [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of hello **Redis Cache** blade.</span></span>

<span data-ttu-id="1f113-218">Каждая ценовая категория имеет различные ограничения для количества клиентских подключений, памяти и пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="1f113-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="1f113-219">Если в течение продолжительного периода времени кэш приближается к максимальной емкости для этих метрик, создается рекомендация.</span><span class="sxs-lookup"><span data-stu-id="1f113-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="1f113-220">Дополнительные сведения о метрики hello и проверены hello ограничения **рекомендации** , см. в следующей таблице hello:</span><span class="sxs-lookup"><span data-stu-id="1f113-220">For more information about hello metrics and limits reviewed by hello **Recommendations** tool, see hello following table:</span></span>

| <span data-ttu-id="1f113-221">Метрика "Кэш Redis"</span><span class="sxs-lookup"><span data-stu-id="1f113-221">Redis Cache metric</span></span> | <span data-ttu-id="1f113-222">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="1f113-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="1f113-223">Пропускная способность сети</span><span class="sxs-lookup"><span data-stu-id="1f113-223">Network bandwidth usage</span></span> |[<span data-ttu-id="1f113-224">Производительность кэша — доступная пропускная способность</span><span class="sxs-lookup"><span data-stu-id="1f113-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="1f113-225">Подключенные клиенты</span><span class="sxs-lookup"><span data-stu-id="1f113-225">Connected clients</span></span> |[<span data-ttu-id="1f113-226">Конфигурация сервера Redis по умолчанию — максимальное количество клиентов</span><span class="sxs-lookup"><span data-stu-id="1f113-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="1f113-227">Загрузка сервера</span><span class="sxs-lookup"><span data-stu-id="1f113-227">Server load</span></span> |[<span data-ttu-id="1f113-228">Диаграммы использования — загрузка сервера Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="1f113-229">Использование памяти</span><span class="sxs-lookup"><span data-stu-id="1f113-229">Memory usage</span></span> |[<span data-ttu-id="1f113-230">Производительность кэша — размер</span><span class="sxs-lookup"><span data-stu-id="1f113-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="1f113-231">tooupgrade кэша, нажмите кнопку **обновление** toochange hello ценовой категории и [шкалы](#scale) кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-231">tooupgrade your cache, click **Upgrade now** toochange hello pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="1f113-232">Дополнительные сведения о выборе ценовой категории кэша см. в разделе [Какое предложение и размер кэша Redis мне следует использовать?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="1f113-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="1f113-233">Масштаб</span><span class="sxs-lookup"><span data-stu-id="1f113-233">Scale</span></span>
<span data-ttu-id="1f113-234">Нажмите кнопку **шкалы** hello tooview или измените ценовую категорию для вашего кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-234">Click **Scale** tooview or change hello pricing tier for your cache.</span></span> <span data-ttu-id="1f113-235">Дополнительные сведения о масштабировании см. в разделе [как tooScale Redis для Azure кэшировать](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-235">For more information on scaling, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Ценовая категория кэша Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="1f113-237">Размер кластера Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-237">Redis Cluster Size</span></span>
<span data-ttu-id="1f113-238">Нажмите кнопку **размер кластера Redis (Предварительная версия)** размер кластера hello toochange для выполнения расширенной кэш с включенной кластеризацией.</span><span class="sxs-lookup"><span data-stu-id="1f113-238">Click **(PREVIEW) Redis Cluster Size** toochange hello cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="1f113-239">Обратите внимание, что при hello Azure Redis кэша Premium уровня был выпущен tooGeneral доступности функции hello Redis размер кластера в настоящее время находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="1f113-239">Note that while hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Размер кластера Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="1f113-241">размер кластера toochange hello, используйте ползунок hello, или введите число от 1 до 10 в hello **количества сегментов** текстовое поле и нажмите кнопку **ОК** toosave.</span><span class="sxs-lookup"><span data-stu-id="1f113-241">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f113-242">Кластеризация Redis доступна только для кэша категории «Премиум».</span><span class="sxs-lookup"><span data-stu-id="1f113-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="1f113-243">Дополнительные сведения см. в разделе [как tooconfigure кластеризации для кэша Redis Azure Premium](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-243">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="1f113-244">Сохраняемость данных Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-244">Redis data persistence</span></span>
<span data-ttu-id="1f113-245">Нажмите кнопку **сохраняемости данных Redis** tooenable, отключить или настроить сохранение данных кэша premium.</span><span class="sxs-lookup"><span data-stu-id="1f113-245">Click **Redis data persistence** tooenable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="1f113-246">Кэш Redis для Azure обеспечивает сохраняемость Redis на основе [RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) или [AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="1f113-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="1f113-247">Дополнительные сведения см. в разделе [как tooconfigure сохраняемости для кэша Redis Azure Premium](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-247">For more information, see [How tooconfigure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="1f113-248">Сохраняемость данных Redis доступна только для кэшей категории «Премиум».</span><span class="sxs-lookup"><span data-stu-id="1f113-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="1f113-249">запланировать обновления</span><span class="sxs-lookup"><span data-stu-id="1f113-249">Schedule updates</span></span>
<span data-ttu-id="1f113-250">Hello **расписание обновления** колонке позволяет toodesignate периода обслуживания для обновления сервера Redis своего кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-250">hello **Schedule updates** blade allows you toodesignate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1f113-251">Hello окна обслуживания применяется только tooRedis обновления сервера и не tooany Azure обновлений или обновления операционной системы toohello hello виртуальных машин, которые размещения кэша hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-251">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![запланировать обновления](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="1f113-253">toospecify периода обслуживания, проверьте дни hello требуемого укажите hello час запуска окна обслуживания для каждого дня и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1f113-253">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="1f113-254">Обратите внимание, что период обслуживания hello в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="1f113-254">Note that hello maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1f113-255">Hello **расписание обновления** функция доступна только для кэши уровня Premium.</span><span class="sxs-lookup"><span data-stu-id="1f113-255">hello **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="1f113-256">Дополнительные сведения и указания см. в разделе о [планировании обновлений](cache-administration.md#schedule-updates) статьи, посвященной администрированию кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="1f113-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="1f113-257">Георепликация</span><span class="sxs-lookup"><span data-stu-id="1f113-257">Geo-replication</span></span>

<span data-ttu-id="1f113-258">Hello **георепликации** колонке предоставляет механизм для связывания двух экземпляров кэша Redis для Azure уровня Premium.</span><span class="sxs-lookup"><span data-stu-id="1f113-258">hello **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="1f113-259">Один кэш используется в качестве основных связанный кэш hello и hello других получателей связанного кэширования hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-259">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="1f113-260">Hello дополнительных связанных кэш становится доступным только для чтения и репликации данных, является запись toohello основных кэш toohello дополнительных связанный кэш.</span><span class="sxs-lookup"><span data-stu-id="1f113-260">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="1f113-261">Эта возможность может быть используется tooreplicate кэша в разных регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="1f113-261">This functionality can be used tooreplicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f113-262">**Георепликация** доступна только для кэшей категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1f113-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="1f113-263">Дополнительные сведения и инструкции см. в разделе [как tooconfigure географической репликации для кэша Azure Redis](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-263">For more information and instructions, see [How tooconfigure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="1f113-264">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="1f113-264">Virtual Network</span></span>
<span data-ttu-id="1f113-265">Hello **виртуальной сети** раздел позволяет вам tooconfigure hello виртуальной сети настроек для кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-265">hello **Virtual Network** section allows you tooconfigure hello virtual network settings for your cache.</span></span> <span data-ttu-id="1f113-266">Сведения о создании кэша premium с помощью виртуальной сети поддержки и обновления ее параметров, в разделе [как tooconfigure виртуальная сеть поддерживает для кэша Redis Azure Premium](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-266">For information on creating a premium cache with VNET support and updating its settings, see [How tooconfigure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f113-267">Параметры виртуальной сети доступны только для кэшей уровня Премиум, которые были настроены с поддержкой виртуальной сети во время создания кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="1f113-268">Брандмауэр</span><span class="sxs-lookup"><span data-stu-id="1f113-268">Firewall</span></span>

<span data-ttu-id="1f113-269">Нажмите кнопку **брандмауэра** tooview и настройка правил брандмауэра для кэша Redis Azure Premium.</span><span class="sxs-lookup"><span data-stu-id="1f113-269">Click **Firewall** tooview and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Брандмауэр](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="1f113-271">В правилах брандмауэра можно указать начало и конец диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1f113-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="1f113-272">Если настроены правила брандмауэра, подключений клиентов только из hello указано диапазоны IP-адресов можно подключиться toohello кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-272">When firewall rules are configured, only client connections from hello specified IP address ranges can connect toohello cache.</span></span> <span data-ttu-id="1f113-273">При сохранении правила брандмауэра нет небольшая задержка перед hello правило вступает в силу.</span><span class="sxs-lookup"><span data-stu-id="1f113-273">When a firewall rule is saved there is a short delay before hello rule is effective.</span></span> <span data-ttu-id="1f113-274">Обычно эта задержка не длится более одной минуты.</span><span class="sxs-lookup"><span data-stu-id="1f113-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f113-275">Подключения из систем мониторинга кэша Redis для Azure всегда разрешены, даже если настроены правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="1f113-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="1f113-276">Правила брандмауэра доступны только для кэшей уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1f113-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="1f113-277">Свойства</span><span class="sxs-lookup"><span data-stu-id="1f113-277">Properties</span></span>
<span data-ttu-id="1f113-278">Нажмите кнопку **свойства** tooview сведения о кэше, включая конечную точку кэша hello и порты.</span><span class="sxs-lookup"><span data-stu-id="1f113-278">Click **Properties** tooview information about your cache, including hello cache endpoint and ports.</span></span>

![Свойства кэша Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="1f113-280">Блокировки</span><span class="sxs-lookup"><span data-stu-id="1f113-280">Locks</span></span>
<span data-ttu-id="1f113-281">Hello **блокирует** раздел позволяет вам toolock подписки, группы ресурсов или ресурсов tooprevent другим пользователям в организации от случайного удаления или изменения критическим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="1f113-281">hello **Locks** section allows you toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="1f113-282">Дополнительные сведения см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="1f113-283">Сценарий автоматизации</span><span class="sxs-lookup"><span data-stu-id="1f113-283">Automation script</span></span>

<span data-ttu-id="1f113-284">Нажмите кнопку **сценарий автоматизации** toobuild и экспортировать шаблон развернутых ресурсов для будущих развертываний.</span><span class="sxs-lookup"><span data-stu-id="1f113-284">Click **Automation script** toobuild and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="1f113-285">Дополнительные сведения о работе с шаблонами см. в статье [Развертывание ресурсов с использованием шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="1f113-286">Параметры администрирования</span><span class="sxs-lookup"><span data-stu-id="1f113-286">Administration settings</span></span>
<span data-ttu-id="1f113-287">Здравствуйте, параметры в hello **администрирования** раздел разрешить hello tooperform следующие административные задачи для кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-287">hello settings in hello **Administration** section allow you tooperform hello following administrative tasks for your cache.</span></span> 

![Администрирование](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="1f113-289">Импорт данных</span><span class="sxs-lookup"><span data-stu-id="1f113-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="1f113-290">Экспорт данных</span><span class="sxs-lookup"><span data-stu-id="1f113-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="1f113-291">Reboot</span><span class="sxs-lookup"><span data-stu-id="1f113-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="1f113-292">Импорт и экспорт</span><span class="sxs-lookup"><span data-stu-id="1f113-292">Import/Export</span></span>
<span data-ttu-id="1f113-293">Импорт и экспорт является операцией управления данных кэша Redis для Azure, позволяющий tooimport и экспорт данных в кэше hello, Импорт и экспорт моментального снимка Redis кэша базы данных (RDB) из premium кэша tooa страничный большой двоичный объект в учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1f113-293">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport and export data in hello cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa page blob in an Azure Storage Account.</span></span> <span data-ttu-id="1f113-294">Импорт и экспорт позволяет toomigrate между различными экземплярами кэша Redis для Azure или заполнения кэша hello с данными, перед использованием.</span><span class="sxs-lookup"><span data-stu-id="1f113-294">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="1f113-295">Импорт может быть используется toobring Redis совместимые RDB файлы с любого сервера Redis под управлением какой-либо облаке или в среде, включая Redis под управлением Linux, Windows или любого поставщика облачных служб, таких как Amazon Web Services и другие.</span><span class="sxs-lookup"><span data-stu-id="1f113-295">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="1f113-296">Импорт данных — простой способ toocreate кэша заполнены данными.</span><span class="sxs-lookup"><span data-stu-id="1f113-296">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="1f113-297">Во время процесса импорта hello кэша Redis для Azure hello RDB файлы загружаются из хранилища Azure в память и затем вставляет hello ключи в кэш hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-297">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory, and then inserts hello keys into hello cache.</span></span>

<span data-ttu-id="1f113-298">Экспорт позволяет tooexport hello данные, хранящиеся в кэш Azure Redis tooRedis совместимые файлы RDB.</span><span class="sxs-lookup"><span data-stu-id="1f113-298">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB files.</span></span> <span data-ttu-id="1f113-299">Можно использовать данные toomove этого компонента из одной tooanother экземпляр кэша Redis для Azure или tooanother сервера Redis.</span><span class="sxs-lookup"><span data-stu-id="1f113-299">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="1f113-300">Во время процесса экспорта hello временный файл создается на hello виртуальной Машины, что узлы hello экземпляр сервера кэша Redis для Azure, а hello файл отправленного toohello, назначенные учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="1f113-300">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="1f113-301">После завершения операции экспорта hello состояние успеха или сбоя hello временный файл удаляется.</span><span class="sxs-lookup"><span data-stu-id="1f113-301">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f113-302">Функция импорта и экспорта доступна только для кэшей категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1f113-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="1f113-303">Дополнительные сведения и указания см. в статье [Импорт и экспорт данных в кэше Redis для Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="1f113-304">Reboot</span><span class="sxs-lookup"><span data-stu-id="1f113-304">Reboot</span></span>
<span data-ttu-id="1f113-305">Hello **перезагрузить** колонке позволяет tooreboot hello узлов кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-305">hello **Reboot** blade allows you tooreboot hello nodes of your cache.</span></span> <span data-ttu-id="1f113-306">Это перезагрузка дает вам tootest приложения для обеспечения устойчивости при наличии сбоя узла кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-306">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="1f113-308">При наличии кэша premium с включенной кластеризацией, можно выбрать какие сегменты кэша tooreboot hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-308">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="1f113-310">tooreboot один или несколько узлов кэша, выберите узлы требуемого hello и нажмите кнопку **перезагрузки**.</span><span class="sxs-lookup"><span data-stu-id="1f113-310">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="1f113-311">При наличии кэша premium с включенной кластеризацией выберите tooreboot сегментам hello и нажмите кнопку **перезагрузки**.</span><span class="sxs-lookup"><span data-stu-id="1f113-311">If you have a premium cache with clustering enabled, select hello shard(s) tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="1f113-312">Через несколько минут hello выбранные узлы перезагрузку и снова подключены к сети через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1f113-312">After a few minutes, hello selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f113-313">Перезагрузка теперь доступна для всех ценовых категорий.</span><span class="sxs-lookup"><span data-stu-id="1f113-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="1f113-314">Дополнительные сведения и указания см. в разделе о [перезагрузке](cache-administration.md#reboot) статьи, посвященной администрированию кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="1f113-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="1f113-315">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="1f113-315">Monitoring</span></span>

<span data-ttu-id="1f113-316">Hello **мониторинг** раздел позволяет вам tooconfigure диагностики и мониторинга для кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="1f113-316">hello **Monitoring** section allows you tooconfigure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="1f113-317">Дополнительные сведения о кэше Redis для Azure наблюдение и диагностику см. в разделе [как toomonitor Redis для Azure кэшировать](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How toomonitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Диагностика](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="1f113-319">Метрики Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="1f113-320">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="1f113-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="1f113-321">Диагностика</span><span class="sxs-lookup"><span data-stu-id="1f113-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="1f113-322">Метрики Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-322">Redis metrics</span></span>
<span data-ttu-id="1f113-323">Нажмите кнопку **Redis метрики** слишком[Просмотр метрик](cache-how-to-monitor.md#view-cache-metrics) своего кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-323">Click **Redis metrics** too[view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="1f113-324">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="1f113-324">Alert rules</span></span>

<span data-ttu-id="1f113-325">Нажмите кнопку **предупреждения правила** tooconfigure оповещения на основе кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="1f113-325">Click **Alert rules** tooconfigure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="1f113-326">Дополнительные сведения см. в статье [Как отслеживать кэш Redis для Azure](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="1f113-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="1f113-327">Диагностика</span><span class="sxs-lookup"><span data-stu-id="1f113-327">Diagnostics</span></span>

<span data-ttu-id="1f113-328">По умолчанию в Azure Monitor метрики кэша [хранятся в течение 30 дней](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive), а затем удаляются.</span><span class="sxs-lookup"><span data-stu-id="1f113-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="1f113-329">Щелкните toopersist показатели кэша более 30 дней **диагностики** слишком[Настройка учетной записи хранения hello](cache-how-to-monitor.md#export-cache-metrics) используется toostore диагностики кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-329">toopersist your cache metrics for longer than 30 days, click **Diagnostics** too[configure hello storage account](cache-how-to-monitor.md#export-cache-metrics) used toostore cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="1f113-330">В дополнение tooarchiving toostorage метрик вашего кэша, вы также можете [поток их tooan концентратора событий или отправлять их tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="1f113-330">In addition tooarchiving your cache metrics toostorage, you can also [stream them tooan Event hub or send them tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="1f113-331">Настройки поддержки и устранения неполадок</span><span class="sxs-lookup"><span data-stu-id="1f113-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="1f113-332">Здравствуйте, параметры в hello **поддержки + Устранение неполадок** раздела предоставляют параметры для устранения проблем с кэшем.</span><span class="sxs-lookup"><span data-stu-id="1f113-332">hello settings in hello **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Поддержка и устранение неполадок](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="1f113-334">Работоспособность ресурса</span><span class="sxs-lookup"><span data-stu-id="1f113-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="1f113-335">Новый запрос в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="1f113-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="1f113-336">Работоспособность ресурса</span><span class="sxs-lookup"><span data-stu-id="1f113-336">Resource health</span></span>
<span data-ttu-id="1f113-337">Служба **работоспособности ресурсов** отслеживает ресурс и сообщает, работает ли он как ожидалось.</span><span class="sxs-lookup"><span data-stu-id="1f113-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="1f113-338">Дополнительные сведения о hello службы работоспособности ресурсов Azure см. в разделе [Обзор работоспособности ресурсов Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-338">For more information about hello Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1f113-339">Состояние ресурса — в настоящее время не удается tooreport о работоспособности hello экземплярами кэша Redis для Azure, размещенными в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="1f113-339">Resource health is currently unable tooreport on hello health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="1f113-340">Дополнительные сведения см. в разделе [Все ли функции кэша работают, когда он размещен в виртуальной сети?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet).</span><span class="sxs-lookup"><span data-stu-id="1f113-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="1f113-341">Новый запрос на техническую поддержку</span><span class="sxs-lookup"><span data-stu-id="1f113-341">New support request</span></span>
<span data-ttu-id="1f113-342">Нажмите кнопку **New поддержки запроса** tooopen запрос на поддержку своего кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-342">Click **New support request** tooopen a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="1f113-343">Конфигурация сервера Redis по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1f113-343">Default Redis server configuration</span></span>
<span data-ttu-id="1f113-344">Новые экземпляры кэша Redis для Azure настроены следующие значения конфигурации Redis по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-344">New Azure Redis Cache instances are configured with hello following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="1f113-345">Параметры Hello в данном разделе нельзя изменить при помощи hello `StackExchange.Redis.IServer.ConfigSet` метод.</span><span class="sxs-lookup"><span data-stu-id="1f113-345">hello settings in this section cannot be changed using hello `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="1f113-346">Если этот метод вызывается с одним hello команды в этом разделе, выдается исключение аналогичные toohello следующие:</span><span class="sxs-lookup"><span data-stu-id="1f113-346">If this method is called with one of hello commands in this section, an exception similar toohello following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="1f113-347">Все значения, которые можно настроить, например **максимум памяти политики**, настраиваемых с помощью hello портал Azure и управление из командной строки, таких как Azure CLI или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f113-347">Any values that are configurable, such as **max-memory-policy**, are configurable through hello Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="1f113-348">Настройка</span><span class="sxs-lookup"><span data-stu-id="1f113-348">Setting</span></span> | <span data-ttu-id="1f113-349">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1f113-349">Default value</span></span> | <span data-ttu-id="1f113-350">Описание</span><span class="sxs-lookup"><span data-stu-id="1f113-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="1f113-351">16</span><span class="sxs-lookup"><span data-stu-id="1f113-351">16</span></span> |<span data-ttu-id="1f113-352">количество баз данных по умолчанию Hello равно 16, но можно настроить разные номера на основе hello ценовой категории. <sup>1</sup> база данных по умолчанию hello-DB 0, можно выбрать его для подключения с помощью `connection.GetDatabase(dbid)` где `dbid` является числом в диапазоне от `0` и `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="1f113-352">hello default number of databases is 16 but you can configure a different number based on hello pricing tier.<sup>1</sup> hello default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="1f113-353">Зависит от ценового уровня hello<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="1f113-353">Depends on hello pricing tier<sup>2</sup></span></span> |<span data-ttu-id="1f113-354">Это максимальное количество подключенных клиентов, одновременно hello же hello времени.</span><span class="sxs-lookup"><span data-stu-id="1f113-354">This is hello maximum number of connected clients allowed at hello same time.</span></span> <span data-ttu-id="1f113-355">После достижения предела hello Redis закрывает все новые соединения hello вернуть ошибку «максимальное количество клиентов достигнут».</span><span class="sxs-lookup"><span data-stu-id="1f113-355">Once hello limit is reached Redis closes all hello new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="1f113-356">Политика Maxmemory является приветствия для как Redis выбирает, какие tooremove при `maxmemory` достигается (hello размер предложения, выбранный при создании кэша hello hello кэша).</span><span class="sxs-lookup"><span data-stu-id="1f113-356">Maxmemory policy is hello setting for how Redis selects what tooremove when `maxmemory` (hello size of hello cache offering you selected when you created hello cache) is reached.</span></span> <span data-ttu-id="1f113-357">По умолчанию hello кэша Redis для Azure — параметр `volatile-lru`, который удаляет hello ключи со сроком действия, заданные с помощью алгоритма LRU.</span><span class="sxs-lookup"><span data-stu-id="1f113-357">With Azure Redis Cache hello default setting is `volatile-lru`, which removes hello keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="1f113-358">Этот параметр можно настроить в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1f113-358">This setting can be configured in hello Azure portal.</span></span> <span data-ttu-id="1f113-359">Дополнительные сведения см. в разделе [Политики памяти](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="1f113-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="1f113-360">3</span><span class="sxs-lookup"><span data-stu-id="1f113-360">3</span></span> |<span data-ttu-id="1f113-361">toosave памяти, LRU и минимальный TTL алгоритмы являются примерные алгоритмы вместо точными.</span><span class="sxs-lookup"><span data-stu-id="1f113-361">toosave memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="1f113-362">По умолчанию Redis проверок три ключей и получает hello один менее недавно использованного.</span><span class="sxs-lookup"><span data-stu-id="1f113-362">By default Redis checks three keys and picks hello one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="1f113-363">5 000</span><span class="sxs-lookup"><span data-stu-id="1f113-363">5,000</span></span> |<span data-ttu-id="1f113-364">Максимальное время выполнения сценария Lua в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="1f113-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="1f113-365">При достижении максимального времени выполнения hello Redis регистрирует скрипт по-прежнему выполнения после hello максимально допустимое время, которое запускает tooreply tooqueries с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="1f113-365">If hello maximum execution time is reached, Redis logs that a script is still in execution after hello maximum allowed time, and starts tooreply tooqueries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="1f113-366">500</span><span class="sxs-lookup"><span data-stu-id="1f113-366">500</span></span> |<span data-ttu-id="1f113-367">Максимальный размер очереди событий сценариев.</span><span class="sxs-lookup"><span data-stu-id="1f113-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="1f113-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="1f113-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="1f113-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="1f113-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="1f113-370">Hello ограничения буферов вывода клиентов можно использовать tooforce отключения клиентов, не считываются данные с сервера hello достаточно быстро для какой-либо причине (как правило, причиной является клиента Pub/Sub не могут использовать столь же быстро, как их производит издатель hello сообщения).</span><span class="sxs-lookup"><span data-stu-id="1f113-370">hello client output buffer limits can be used tooforce disconnection of clients that are not reading data from hello server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as hello publisher can produce them).</span></span> <span data-ttu-id="1f113-371">Дополнительные сведения см. по ссылке [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="1f113-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="1f113-372"><a name="databases"></a>
<sup>1</sup>ограничение hello `databases` отличается для каждого кэша Azure Redis ценовой категории и может быть задано при создании кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-372"><a name="databases"></a>
<sup>1</sup>hello limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="1f113-373">Если не `databases` указан параметр во время создания кэша по умолчанию hello — 16.</span><span class="sxs-lookup"><span data-stu-id="1f113-373">If no `databases` setting is specified during cache creation, hello default is 16.</span></span>

* <span data-ttu-id="1f113-374">Кэши уровней Basic и Standard</span><span class="sxs-lookup"><span data-stu-id="1f113-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="1f113-375">C0 (250 МБ) кэша — копирование баз данных too16</span><span class="sxs-lookup"><span data-stu-id="1f113-375">C0 (250 MB) cache - up too16 databases</span></span>
  * <span data-ttu-id="1f113-376">C1 кэша (1 ГБ) — копирование баз данных too16</span><span class="sxs-lookup"><span data-stu-id="1f113-376">C1 (1 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="1f113-377">C2 кэша (2,5 ГБ) — копирование баз данных too16</span><span class="sxs-lookup"><span data-stu-id="1f113-377">C2 (2.5 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="1f113-378">C3 кэша (6 ГБ) — копирование баз данных too16</span><span class="sxs-lookup"><span data-stu-id="1f113-378">C3 (6 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="1f113-379">C4 кэша (13 ГБ) — копирование баз данных too32</span><span class="sxs-lookup"><span data-stu-id="1f113-379">C4 (13 GB) cache - up too32 databases</span></span>
  * <span data-ttu-id="1f113-380">C5 кэша (26 ГБ) — копирование баз данных too48</span><span class="sxs-lookup"><span data-stu-id="1f113-380">C5 (26 GB) cache - up too48 databases</span></span>
  * <span data-ttu-id="1f113-381">C6 кэша (53 ГБ) — копирование баз данных too64</span><span class="sxs-lookup"><span data-stu-id="1f113-381">C6 (53 GB) cache - up too64 databases</span></span>
* <span data-ttu-id="1f113-382">Кэши уровня Premium</span><span class="sxs-lookup"><span data-stu-id="1f113-382">Premium caches</span></span>
  * <span data-ttu-id="1f113-383">P1 (6 ГБ — 60 ГБ) — копирование баз данных too16</span><span class="sxs-lookup"><span data-stu-id="1f113-383">P1 (6 GB - 60 GB) - up too16 databases</span></span>
  * <span data-ttu-id="1f113-384">P2 (13-130 ГБ) — копирование баз данных too32</span><span class="sxs-lookup"><span data-stu-id="1f113-384">P2 (13 GB - 130 GB) - up too32 databases</span></span>
  * <span data-ttu-id="1f113-385">P3 (26 ГБ — 260 ГБ) — копирование баз данных too48</span><span class="sxs-lookup"><span data-stu-id="1f113-385">P3 (26 GB - 260 GB) - up too48 databases</span></span>
  * <span data-ttu-id="1f113-386">P4 (53-530 ГБ) — копирование баз данных too64</span><span class="sxs-lookup"><span data-stu-id="1f113-386">P4 (53 GB - 530 GB) - up too64 databases</span></span>
  * <span data-ttu-id="1f113-387">Все кэши premium с кластером Redis enabled - Redis кластера поддерживает только использование базы данных 0, поэтому hello `databases` для любого кэша premium с кластером Redis включена равняется 1 и hello предела [выберите](http://redis.io/commands/select) команды не разрешено.</span><span class="sxs-lookup"><span data-stu-id="1f113-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so hello `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and hello [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="1f113-388">Дополнительные сведения см. в разделе [необходимо toomake любые изменения toomy клиентского приложения toouse кластеризации?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="1f113-388">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="1f113-389">Дополнительные сведения о базах данных см. в разделе [Что такое базы данных Redis?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="1f113-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="1f113-390">Hello `databases` параметр может быть настроена только во время создания кэша и только с помощью PowerShell, CLI или других клиентов управления.</span><span class="sxs-lookup"><span data-stu-id="1f113-390">hello `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="1f113-391">Пример настройки `databases` во время создания кэша с помощью PowerShell см. в разделе о командлете [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="1f113-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="1f113-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` отличается для каждой ценовой категории кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="1f113-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="1f113-393">Кэши уровней Basic и Standard</span><span class="sxs-lookup"><span data-stu-id="1f113-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="1f113-394">C0 (250 МБ) кэша - too256 подключения</span><span class="sxs-lookup"><span data-stu-id="1f113-394">C0 (250 MB) cache - up too256 connections</span></span>
  * <span data-ttu-id="1f113-395">C1 кэш (1 ГБ) — копирование too1, 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1f113-395">C1 (1 GB) cache - up too1,000 connections</span></span>
  * <span data-ttu-id="1f113-396">C2 кэш (2,5 ГБ) — копирование too2, 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1f113-396">C2 (2.5 GB) cache - up too2,000 connections</span></span>
  * <span data-ttu-id="1f113-397">C3 кэш (6 ГБ) — копирование too5, 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1f113-397">C3 (6 GB) cache - up too5,000 connections</span></span>
  * <span data-ttu-id="1f113-398">C4 кэш (13 ГБ) — копирование too10, 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1f113-398">C4 (13 GB) cache - up too10,000 connections</span></span>
  * <span data-ttu-id="1f113-399">C5 кэш (26 ГБ) — копирование too15, 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1f113-399">C5 (26 GB) cache - up too15,000 connections</span></span>
  * <span data-ttu-id="1f113-400">C6 кэш (53 ГБ) — копирование too20, 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1f113-400">C6 (53 GB) cache - up too20,000 connections</span></span>
* <span data-ttu-id="1f113-401">Кэши уровня Premium</span><span class="sxs-lookup"><span data-stu-id="1f113-401">Premium caches</span></span>
  * <span data-ttu-id="1f113-402">P1 (6 ГБ — 60 ГБ) — копирование too7 подключения на скорости 500</span><span class="sxs-lookup"><span data-stu-id="1f113-402">P1 (6 GB - 60 GB) - up too7,500 connections</span></span>
  * <span data-ttu-id="1f113-403">P2 (13-130 ГБ) — копирование too15 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1f113-403">P2 (13 GB - 130 GB) - up too15,000 connections</span></span>
  * <span data-ttu-id="1f113-404">P3 (26 ГБ — 260 ГБ) — копирование too30 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1f113-404">P3 (26 GB - 260 GB) - up too30,000 connections</span></span>
  * <span data-ttu-id="1f113-405">P4 (53-530 ГБ) — копирование too40 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1f113-405">P4 (53 GB - 530 GB) - up too40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="1f113-406">Хотя каждый размер кэша позволяет *до* определенное количество соединений, каждого подключения tooRedis издержки связан.</span><span class="sxs-lookup"><span data-stu-id="1f113-406">While each size of cache allows *up to* a certain number of connections, each connection tooRedis has overhead associated with it.</span></span> <span data-ttu-id="1f113-407">Примером таких накладных расходов могут служить загрузка ЦП и использование памяти в результате шифрования TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="1f113-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="1f113-408">Hello максимальное количество подключений для размера кэша предполагается со слабой загрузкой кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-408">hello maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="1f113-409">Если загрузить из соединения издержки *, а также* нагрузки от операции клиента превышает лимит, определенный для системы hello, hello кэша могут возникать проблемы производительности, даже если не превышено ограничение числа подключений hello для hello текущий размер кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-409">If load from connection overhead *plus* load from client operations exceeds capacity for hello system, hello cache can experience capacity issues even if you have not exceeded hello connection limit for hello current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="1f113-410">Команды Redis не поддерживаются в кэше Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="1f113-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1f113-411">Поскольку конфигурации и управления экземплярами кэша Redis для Azure управляется корпорацией Майкрософт, hello отключаются следующие команды.</span><span class="sxs-lookup"><span data-stu-id="1f113-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, hello following commands are disabled.</span></span> <span data-ttu-id="1f113-412">Если при попытке tooinvoke их, появляется сообщение об ошибке слишком`"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="1f113-412">If you try tooinvoke them, you receive an error message similar too`"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="1f113-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="1f113-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="1f113-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="1f113-414">BGSAVE</span></span>
> * <span data-ttu-id="1f113-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="1f113-415">CONFIG</span></span>
> * <span data-ttu-id="1f113-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="1f113-416">DEBUG</span></span>
> * <span data-ttu-id="1f113-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="1f113-417">MIGRATE</span></span>
> * <span data-ttu-id="1f113-418">Сохранить</span><span class="sxs-lookup"><span data-stu-id="1f113-418">SAVE</span></span>
> * <span data-ttu-id="1f113-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="1f113-419">SHUTDOWN</span></span>
> * <span data-ttu-id="1f113-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="1f113-420">SLAVEOF</span></span>
> * <span data-ttu-id="1f113-421">CLUSTER — команды записи для кластера отключены, однако допускается использование кластерных команд только для чтения.</span><span class="sxs-lookup"><span data-stu-id="1f113-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="1f113-422">Дополнительные сведения о командах Redis см. по ссылке [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="1f113-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="1f113-423">Консоль Redis</span><span class="sxs-lookup"><span data-stu-id="1f113-423">Redis console</span></span>
<span data-ttu-id="1f113-424">Можно безопасно выполнить команды tooyour экземпляров кэша Redis для Azure, с помощью hello **Redis консоли**, который доступен в hello портал Azure для всех уровней кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-424">You can securely issue commands tooyour Azure Redis Cache instances using hello **Redis Console**, which is available in hello Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="1f113-425">Hello Redis консоль не работает с [VNET](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-425">hello Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="1f113-426">Когда кэш является частью виртуальной сети, только клиенты в hello виртуальной сети можно обращается к кэшу hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-426">When your cache is part of a VNET, only clients in hello VNET can access hello cache.</span></span> <span data-ttu-id="1f113-427">Поскольку консоль Redis выполняется в вашей локальной браузера, который находится за пределами hello виртуальной сети, она не может подключиться tooyour кэша.</span><span class="sxs-lookup"><span data-stu-id="1f113-427">Because Redis Console runs in your local browser, which is outside hello VNET, it can't connect tooyour cache.</span></span>
> - <span data-ttu-id="1f113-428">В кэше Redis для Azure поддерживаются не все команды Redis.</span><span class="sxs-lookup"><span data-stu-id="1f113-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="1f113-429">Список команд Redis, отключены для кэша Redis для Azure см. в разделе hello предыдущих [команды не поддерживается в кэше Redis для Azure Redis](#redis-commands-not-supported-in-azure-redis-cache) раздела.</span><span class="sxs-lookup"><span data-stu-id="1f113-429">For a list of Redis commands that are disabled for Azure Redis Cache, see hello previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="1f113-430">Дополнительные сведения о командах Redis см. по ссылке [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="1f113-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="1f113-431">hello tooaccess Redis консоли, нажмите кнопку **консоли** из hello **кэша Redis** колонку.</span><span class="sxs-lookup"><span data-stu-id="1f113-431">tooaccess hello Redis Console, click **Console** from hello **Redis Cache** blade.</span></span>

![Консоль Redis](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="1f113-433">tooissue команды для экземпляра кэша, просто hello тип требуемой команды в консоль hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-433">tooissue commands against your cache instance, simply type hello desired command into hello console.</span></span>

![Консоль Redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="1f113-435">С помощью hello консоль Redis с расширенной кэш кластера</span><span class="sxs-lookup"><span data-stu-id="1f113-435">Using hello Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="1f113-436">Когда кэш с помощью hello консоль Redis с расширенной кластера, могут выдавать команды tooa hello кэша в одном сегменте.</span><span class="sxs-lookup"><span data-stu-id="1f113-436">When using hello Redis Console with a premium clustered cache, you can issue commands tooa single shard of hello cache.</span></span> <span data-ttu-id="1f113-437">tooissue конкретным сегментом tooa команды, сначала подключиться toohello нужному сегменту, щелкнув его в выбора сегментов hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-437">tooissue a command tooa specific shard, first connect toohello desired shard by clicking it on hello shard picker.</span></span>

![Консоль Redis](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="1f113-439">При попытке tooaccess ключ, который хранится в другой сегмент, чем hello подключенных сегментов, появляется ошибка сообщение аналогичные toohello следующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="1f113-439">If you attempt tooaccess a key that is stored in a different shard than hello connected shard, you receive an error message similar toohello following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="1f113-440">В предыдущем примере hello сегмент 1 — hello выбранного сегментов, но `myKey` находится в сегмент 0, как указано в hello `(shard 0)` часть сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="1f113-440">In hello previous example, shard 1 is hello selected shard, but `myKey` is located in shard 0, as indicated by hello `(shard 0)` portion of hello error message.</span></span> <span data-ttu-id="1f113-441">В этом примере tooaccess `myKey`выберите сегмент 0 с помощью hello выбора сегментов, а затем команду hello требуемого проблему.</span><span class="sxs-lookup"><span data-stu-id="1f113-441">In this example, tooaccess `myKey`, select shard 0 using hello shard picker, and then issue hello desired command.</span></span>


## <a name="move-your-cache-tooa-new-subscription"></a><span data-ttu-id="1f113-442">Переместить в новую подписку tooa кэша</span><span class="sxs-lookup"><span data-stu-id="1f113-442">Move your cache tooa new subscription</span></span>
<span data-ttu-id="1f113-443">Можно переместить в новую подписку tooa кэша, щелкнув **переместить**.</span><span class="sxs-lookup"><span data-stu-id="1f113-443">You can move your cache tooa new subscription by clicking **Move**.</span></span>

![Перемещение кэша Redis](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="1f113-445">Сведения о перемещении ресурсов от одного ресурса группы tooanother и из одной подписки tooanother см. в разделе [переместить группу ресурсов toonew ресурсов или подписку](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="1f113-445">For information on moving resources from one resource group tooanother, and from one subscription tooanother, see [Move resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f113-446">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f113-446">Next steps</span></span>
* <span data-ttu-id="1f113-447">Дополнительные сведения о работе с командами Redis см. в разделе [Как выполнять команды Redis?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="1f113-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

