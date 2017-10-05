---
title: "Как настроить кэш Redis для Azure | Документация Майкрософт"
description: "Обзор конфигурации Redis по умолчанию для кэша Redis для Azure и описание способов настройки экземпляров кэша Redis для Azure"
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
ms.openlocfilehash: 0274e58eb2e83202d4dbc58da0c67d0fdde22ede
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-azure-redis-cache"></a><span data-ttu-id="1b092-103">Настройка кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="1b092-103">How to configure Azure Redis Cache</span></span>
<span data-ttu-id="1b092-104">В этом разделе рассказывается, как просмотреть и обновить конфигурацию экземпляров кэша Redis для Azure, и приводится конфигурация сервера Redis по умолчанию для экземпляров кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="1b092-104">This topic describes how to review and update the configuration for your Azure Redis Cache instances, and covers the default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="1b092-105">Дополнительные сведения о настройке и использовании функций кэша уровня "Премиум" см. в статьях [Настройка постоянного хранения для кэша Redis для Azure уровня Премиум](cache-how-to-premium-persistence.md), [Настройка кластеризации для кэша Redis для Azure уровня Премиум](cache-how-to-premium-clustering.md) и [Настройка поддержки виртуальной сети для кэша Redis для Azure уровня Премиум](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-105">For more information on configuring and using premium cache features, see [How to configure persistence](cache-how-to-premium-persistence.md), [How to configure clustering](cache-how-to-premium-clustering.md), and [How to configure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="1b092-106">Настройка параметров кэша Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="1b092-107">Параметры кэша Redis для Azure можно просмотреть и настроить в колонке **Кэш Redis** с помощью **меню ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="1b092-107">Azure Redis Cache settings are viewed and configured on the **Redis Cache** blade using the **Resource Menu**.</span></span>

![Параметры кэша Redis](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="1b092-109">Просмотреть и настроить следующие параметры можно с помощью **меню ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="1b092-109">You can view and configure the following settings using the **Resource Menu**.</span></span>

* [<span data-ttu-id="1b092-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="1b092-110">Overview</span></span>](#overview)
* [<span data-ttu-id="1b092-111">Журнал действий</span><span class="sxs-lookup"><span data-stu-id="1b092-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="1b092-112">Управление доступом (IAM)</span><span class="sxs-lookup"><span data-stu-id="1b092-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="1b092-113">Теги</span><span class="sxs-lookup"><span data-stu-id="1b092-113">Tags</span></span>](#tags)
* [<span data-ttu-id="1b092-114">Диагностика и решение проблем</span><span class="sxs-lookup"><span data-stu-id="1b092-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="1b092-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="1b092-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="1b092-116">Ключи доступа</span><span class="sxs-lookup"><span data-stu-id="1b092-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="1b092-117">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="1b092-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="1b092-118">Помощник по кэшу Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="1b092-119">Масштабирование</span><span class="sxs-lookup"><span data-stu-id="1b092-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="1b092-120">Размер кластера Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="1b092-121">Сохраняемость данных Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="1b092-122">Планирование обновлений</span><span class="sxs-lookup"><span data-stu-id="1b092-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="1b092-123">Георепликация</span><span class="sxs-lookup"><span data-stu-id="1b092-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="1b092-124">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="1b092-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="1b092-125">Брандмауэр</span><span class="sxs-lookup"><span data-stu-id="1b092-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="1b092-126">Свойства</span><span class="sxs-lookup"><span data-stu-id="1b092-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="1b092-127">Блокировки</span><span class="sxs-lookup"><span data-stu-id="1b092-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="1b092-128">Сценарий автоматизации</span><span class="sxs-lookup"><span data-stu-id="1b092-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="1b092-129">Администрирование</span><span class="sxs-lookup"><span data-stu-id="1b092-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="1b092-130">Импорт данных</span><span class="sxs-lookup"><span data-stu-id="1b092-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="1b092-131">Экспорт данных</span><span class="sxs-lookup"><span data-stu-id="1b092-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="1b092-132">Reboot</span><span class="sxs-lookup"><span data-stu-id="1b092-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="1b092-133">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="1b092-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="1b092-134">Метрики Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="1b092-135">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="1b092-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="1b092-136">Диагностика</span><span class="sxs-lookup"><span data-stu-id="1b092-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="1b092-137">Настройки поддержки и устранения неполадок</span><span class="sxs-lookup"><span data-stu-id="1b092-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="1b092-138">Работоспособность ресурса</span><span class="sxs-lookup"><span data-stu-id="1b092-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="1b092-139">Новый запрос в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="1b092-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="1b092-140">Обзор</span><span class="sxs-lookup"><span data-stu-id="1b092-140">Overview</span></span>

<span data-ttu-id="1b092-141">В разделе **Обзор** содержатся основные сведения о кэше, такие как имя, порты, ценовая категория, и выбранные метрики кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="1b092-142">Журнал действий</span><span class="sxs-lookup"><span data-stu-id="1b092-142">Activity log</span></span>

<span data-ttu-id="1b092-143">Щелкните **Журнал действий**, чтобы просмотреть выполненные с кэшем действия.</span><span class="sxs-lookup"><span data-stu-id="1b092-143">Click **Activity log** to view actions performed on your cache.</span></span> <span data-ttu-id="1b092-144">Также можно использовать фильтрацию, чтобы развернуть это представление, включив в него другие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1b092-144">You can also use filtering to expand this view to include other resources.</span></span> <span data-ttu-id="1b092-145">Дополнительные сведения об использовании журналов аудита см. в статье [Просмотр журналов действий для аудита действий с ресурсами](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="1b092-146">Дополнительные сведения о мониторинге событий кэша Redis для Azure см. в разделе [Операции и оповещения](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="1b092-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="1b092-147">Управление доступом (IAM)</span><span class="sxs-lookup"><span data-stu-id="1b092-147">Access control (IAM)</span></span>

<span data-ttu-id="1b092-148">В разделе **Управление доступом (IAM)** предусматривается поддержка управления доступом на основе ролей (RBAC) на портале Azure, чтобы помочь организациям просто и точно выполнять требования контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="1b092-148">The **Access control (IAM)** section provides support for role-based access control (RBAC) in the Azure portal to help organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="1b092-149">Дополнительные сведения см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-149">For more information, see [Role-based access control in the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="1b092-150">Теги</span><span class="sxs-lookup"><span data-stu-id="1b092-150">Tags</span></span>

<span data-ttu-id="1b092-151">В разделе **Теги** вы можете упорядочить свои ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1b092-151">The **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="1b092-152">Дополнительные сведения см. в статье [Использование тегов для организации ресурсов в Azure](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-152">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="1b092-153">Диагностика и решение проблем</span><span class="sxs-lookup"><span data-stu-id="1b092-153">Diagnose and solve problems</span></span>

<span data-ttu-id="1b092-154">Щелкните **Диагностика и решение проблем** , чтобы узнать об основных проблемах и способах их устранения.</span><span class="sxs-lookup"><span data-stu-id="1b092-154">Click **Diagnose and solve problems** to be provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="1b092-155">Параметры</span><span class="sxs-lookup"><span data-stu-id="1b092-155">Settings</span></span>
<span data-ttu-id="1b092-156">В разделе **Параметры** можно открыть и настроить следующие параметры кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-156">The **Settings** section allows you to access and configure the following settings for your cache.</span></span>

* [<span data-ttu-id="1b092-157">Ключи доступа</span><span class="sxs-lookup"><span data-stu-id="1b092-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="1b092-158">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="1b092-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="1b092-159">Помощник по кэшу Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="1b092-160">Масштабирование</span><span class="sxs-lookup"><span data-stu-id="1b092-160">Scale</span></span>](#scale)
* [<span data-ttu-id="1b092-161">Размер кластера Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="1b092-162">Сохраняемость данных Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="1b092-163">Планирование обновлений</span><span class="sxs-lookup"><span data-stu-id="1b092-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="1b092-164">Георепликация</span><span class="sxs-lookup"><span data-stu-id="1b092-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="1b092-165">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="1b092-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="1b092-166">Брандмауэр</span><span class="sxs-lookup"><span data-stu-id="1b092-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="1b092-167">Свойства</span><span class="sxs-lookup"><span data-stu-id="1b092-167">Properties</span></span>](#properties)
* [<span data-ttu-id="1b092-168">Блокировки</span><span class="sxs-lookup"><span data-stu-id="1b092-168">Locks</span></span>](#locks)
* [<span data-ttu-id="1b092-169">Сценарий автоматизации</span><span class="sxs-lookup"><span data-stu-id="1b092-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="1b092-170">Ключи доступа</span><span class="sxs-lookup"><span data-stu-id="1b092-170">Access keys</span></span>
<span data-ttu-id="1b092-171">Щелкните **Ключи доступа** для отображения или повторного создания ключей доступа для кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-171">Click **Access keys** to view or regenerate the access keys for your cache.</span></span> <span data-ttu-id="1b092-172">Эти ключи используются клиентами, которые подключаются к кэшу.</span><span class="sxs-lookup"><span data-stu-id="1b092-172">These keys are used by the clients connecting to your cache.</span></span>

![Ключи доступа кэша Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="1b092-174">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="1b092-174">Advanced settings</span></span>
<span data-ttu-id="1b092-175">Приведенные ниже параметры доступны в колонке **Дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="1b092-175">The following settings are configured on the **Advanced settings** blade.</span></span>

* [<span data-ttu-id="1b092-176">Порты доступа</span><span class="sxs-lookup"><span data-stu-id="1b092-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="1b092-177">Политики памяти</span><span class="sxs-lookup"><span data-stu-id="1b092-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="1b092-178">Уведомления пространства ключей (дополнительные параметры)</span><span class="sxs-lookup"><span data-stu-id="1b092-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="1b092-179">Порты доступа</span><span class="sxs-lookup"><span data-stu-id="1b092-179">Access Ports</span></span>
<span data-ttu-id="1b092-180">Для новых кэшей без SSL порт по умолчанию отключен.</span><span class="sxs-lookup"><span data-stu-id="1b092-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="1b092-181">Чтобы включить порт, не использующий протокол SSL, в колонке **Дополнительные параметры** для параметра **Разрешить доступ только по SSL** нажмите кнопку **Нет**, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1b092-181">To enable the non-SSL port, click **No** for **Allow access only via SSL** on the **Advanced settings** blade and then click **Save**.</span></span>

![Порты доступа кэша Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="1b092-183">Политики памяти</span><span class="sxs-lookup"><span data-stu-id="1b092-183">Memory policies</span></span>
<span data-ttu-id="1b092-184">Параметры **Политика максимальной памяти**, **maxmemory-reserved** и **maxfragmentationmemory-reserved** в колонке **Дополнительные параметры** позволяют настроить политики памяти для кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-184">The **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on the **Advanced settings** blade configure the memory policies for the cache.</span></span>

![Политика максимальной памяти кэша Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="1b092-186">**Политика максимальной памяти** используется для настройки политики вытеснения для кэша и позволяет выбрать следующие политики вытеснения:</span><span class="sxs-lookup"><span data-stu-id="1b092-186">**Maxmemory policy** configures the eviction policy for the cache and allows you to choose from the following eviction policies:</span></span>

* <span data-ttu-id="1b092-187">`volatile-lru` — значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1b092-187">`volatile-lru` - this is the default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="1b092-188">Дополнительные сведения о политиках `maxmemory` см. в разделе [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies) (Политики вытеснения) на сайте Redis.</span><span class="sxs-lookup"><span data-stu-id="1b092-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="1b092-189">Параметр **maxmemory-reserved** определяет объем памяти в мегабайтах, зарезервированный для операций, не связанных с кэшем, например для репликации при отработке отказов.</span><span class="sxs-lookup"><span data-stu-id="1b092-189">The **maxmemory-reserved** setting configures the amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="1b092-190">Установка этого значения обеспечивает более согласованную работу сервера Redis при изменении нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1b092-190">Setting this value allows you to have a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="1b092-191">Это значение должно быть выше при рабочих нагрузках с преобладанием записи.</span><span class="sxs-lookup"><span data-stu-id="1b092-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="1b092-192">При резервировании памяти для таких операций она недоступна для хранения кэшированных данных.</span><span class="sxs-lookup"><span data-stu-id="1b092-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="1b092-193">Параметр **maxfragmentationmemory-reserved** используется для настройки объема памяти в МБ, который зарезервирован для размещения при фрагментации памяти.</span><span class="sxs-lookup"><span data-stu-id="1b092-193">The **maxfragmentationmemory-reserved** setting configures the amount of memory in MB that is reserved to accommodate for memory fragmentation.</span></span> <span data-ttu-id="1b092-194">Установка этого значения дает возможность более согласованного использования сервера Redis, когда кэш заполнен или почти заполнен, а также при высоком соотношении фрагментации.</span><span class="sxs-lookup"><span data-stu-id="1b092-194">Setting this value allows you to have a more consistent Redis server experience when the cache is full or close to full and the fragmentation ratio is also high.</span></span> <span data-ttu-id="1b092-195">При резервировании памяти для таких операций она недоступна для хранения кэшированных данных.</span><span class="sxs-lookup"><span data-stu-id="1b092-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="1b092-196">При выборе нового значения резервирования памяти (**maxmemory-reserved** или **maxfragmentationmemory-reserved**) также необходимо учитывать, как это изменение может повлиять на кэш, в котором уже выполняется обработка больших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="1b092-196">One thing to consider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="1b092-197">Например, если в кэше емкостью 53 ГБ находится 49 ГБ данных, а вы измените значение параметра резервирования на 8 ГБ, максимальный объем доступной памяти для системы будет снижен до 45 ГБ.</span><span class="sxs-lookup"><span data-stu-id="1b092-197">For instance, if you have a 53 GB cache with 49 GB of data, then change the reservation value to 8 GB, this will drop the max available memory for the system down to 45 GB.</span></span> <span data-ttu-id="1b092-198">Если текущие значения `used_memory` или `used_memory_rss` выше, чем новое ограничение в 45 ГБ, то системе придется вытеснять данные до тех пор, пока оба значения `used_memory` и `used_memory_rss` не станут меньше 45 ГБ.</span><span class="sxs-lookup"><span data-stu-id="1b092-198">If either your current `used_memory` or your `used_memory_rss` values are higher than the new limit of 45 GB, then the system will have to evict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="1b092-199">Вытеснение может увеличить нагрузку на сервер и фрагментацию памяти.</span><span class="sxs-lookup"><span data-stu-id="1b092-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="1b092-200">Дополнительные сведения о доступных метриках кэша, таких как `used_memory` и `used_memory_rss`, см. в разделе [Доступные метрики и интервалы отчетности](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="1b092-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b092-201">Параметры **maxmemory-reserved** и **maxfragmentationmemory-reserved** доступны только для кэшей уровней "Стандартный" и "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1b092-201">The **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="1b092-202">Уведомления пространства ключей (дополнительные параметры)</span><span class="sxs-lookup"><span data-stu-id="1b092-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="1b092-203">В колонке **Дополнительные параметры** можно настроить уведомления пространства ключей Redis.</span><span class="sxs-lookup"><span data-stu-id="1b092-203">Redis keyspace notifications are configured on the **Advanced settings** blade.</span></span> <span data-ttu-id="1b092-204">Уведомления пространства ключей позволяют клиентам получать уведомления при возникновении определенных событий.</span><span class="sxs-lookup"><span data-stu-id="1b092-204">Keyspace notifications allow clients to receive notifications when certain events occur.</span></span>

![Дополнительные параметры кэша Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="1b092-206">Уведомления пространства ключей и параметр **notify-keyspace-events** доступны только для кэшей уровней Standard и Premium.</span><span class="sxs-lookup"><span data-stu-id="1b092-206">Keyspace notifications and the **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="1b092-207">Дополнительные сведения см. в статье [Redis Keyspace Notifications](http://redis.io/topics/notifications) (Уведомления пространства ключей Redis).</span><span class="sxs-lookup"><span data-stu-id="1b092-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="1b092-208">Пример кода см. в файле [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) в примере [Здравствуй, мир!](https://github.com/rustd/RedisSamples/tree/master/HelloWorld).</span><span class="sxs-lookup"><span data-stu-id="1b092-208">For sample code, see the [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in the [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="1b092-209">Помощник по кэшу Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-209">Redis Cache Advisor</span></span>
<span data-ttu-id="1b092-210">В колонке **Помощник по кэшу Redis** отображаются рекомендации для кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-210">The **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="1b092-211">Во время обычной работы не отображается никаких рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="1b092-211">During normal operations, no recommendations are displayed.</span></span> 

![Рекомендации](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="1b092-213">При возникновении во время работы кэша любого из таких условий, как интенсивное использование памяти, пропускной способности сети или сервера, в колонке **Кэш Redis** отображается предупреждение.</span><span class="sxs-lookup"><span data-stu-id="1b092-213">If any conditions occur during the operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on the **Redis Cache** blade.</span></span>

![Рекомендации](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="1b092-215">Дополнительные сведения можно найти в колонке **Рекомендации** .</span><span class="sxs-lookup"><span data-stu-id="1b092-215">Further information can be found on the **Recommendations** blade.</span></span>

![Рекомендации](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="1b092-217">Эти метрики можно отслеживать в колонке **Кэш Redis** в разделах [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) (Диаграммы мониторинга) и [Usage charts](cache-how-to-monitor.md#usage-charts) (Диаграммы использования).</span><span class="sxs-lookup"><span data-stu-id="1b092-217">You can monitor these metrics on the [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of the **Redis Cache** blade.</span></span>

<span data-ttu-id="1b092-218">Каждая ценовая категория имеет различные ограничения для количества клиентских подключений, памяти и пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="1b092-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="1b092-219">Если в течение продолжительного периода времени кэш приближается к максимальной емкости для этих метрик, создается рекомендация.</span><span class="sxs-lookup"><span data-stu-id="1b092-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="1b092-220">Дополнительные сведения о метриках и ограничениях, используемых инструментом **Рекомендации**, см. в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="1b092-220">For more information about the metrics and limits reviewed by the **Recommendations** tool, see the following table:</span></span>

| <span data-ttu-id="1b092-221">Метрика "Кэш Redis"</span><span class="sxs-lookup"><span data-stu-id="1b092-221">Redis Cache metric</span></span> | <span data-ttu-id="1b092-222">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="1b092-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="1b092-223">Пропускная способность сети</span><span class="sxs-lookup"><span data-stu-id="1b092-223">Network bandwidth usage</span></span> |[<span data-ttu-id="1b092-224">Производительность кэша — доступная пропускная способность</span><span class="sxs-lookup"><span data-stu-id="1b092-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="1b092-225">Подключенные клиенты</span><span class="sxs-lookup"><span data-stu-id="1b092-225">Connected clients</span></span> |[<span data-ttu-id="1b092-226">Конфигурация сервера Redis по умолчанию — максимальное количество клиентов</span><span class="sxs-lookup"><span data-stu-id="1b092-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="1b092-227">Загрузка сервера</span><span class="sxs-lookup"><span data-stu-id="1b092-227">Server load</span></span> |[<span data-ttu-id="1b092-228">Диаграммы использования — загрузка сервера Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="1b092-229">Использование памяти</span><span class="sxs-lookup"><span data-stu-id="1b092-229">Memory usage</span></span> |[<span data-ttu-id="1b092-230">Производительность кэша — размер</span><span class="sxs-lookup"><span data-stu-id="1b092-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="1b092-231">Чтобы обновить кэш, нажмите кнопку **Обновить сейчас**. При этом будут изменены ценовая категория и [размер](#scale) кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-231">To upgrade your cache, click **Upgrade now** to change the pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="1b092-232">Дополнительные сведения о выборе ценовой категории кэша см. в разделе [Какое предложение и размер кэша Redis мне следует использовать?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="1b092-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="1b092-233">Масштаб</span><span class="sxs-lookup"><span data-stu-id="1b092-233">Scale</span></span>
<span data-ttu-id="1b092-234">Щелкните **Масштаб**, чтобы просмотреть или изменить ценовую категорию для кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-234">Click **Scale** to view or change the pricing tier for your cache.</span></span> <span data-ttu-id="1b092-235">Дополнительные сведения о масштабировании см. в статье [Масштабирование кэша Redis для Azure](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-235">For more information on scaling, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Ценовая категория кэша Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="1b092-237">Размер кластера Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-237">Redis Cluster Size</span></span>
<span data-ttu-id="1b092-238">Щелкните **Размер кластера Redis (предварительная версия)** , чтобы добавить или удалить сегменты работающего кэша категории "Премиум" с включенной кластеризацией.</span><span class="sxs-lookup"><span data-stu-id="1b092-238">Click **(PREVIEW) Redis Cluster Size** to change the cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="1b092-239">Обратите внимание, что хотя кэш Redis для Azure категории «Премиум» выпущен для общего доступа, сейчас функция изменения размера кластера Redis находится на этапе предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="1b092-239">Note that while the Azure Redis Cache Premium tier has been released to General Availability, the Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Размер кластера Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="1b092-241">Чтобы изменить размер кластера, воспользуйтесь ползунком или введите число от 1 до 10 в текстовом поле **Shard count** (Количество сегментов), а затем нажмите кнопку **ОК** для сохранения изменений.</span><span class="sxs-lookup"><span data-stu-id="1b092-241">To change the cluster size, use the slider or type a number between 1 and 10 in the **Shard count** text box and click **OK** to save.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b092-242">Кластеризация Redis доступна только для кэша категории «Премиум».</span><span class="sxs-lookup"><span data-stu-id="1b092-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="1b092-243">Дополнительные сведения см. в статье [Настройка кластеризации для кэша Redis для Azure уровня Премиум](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-243">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="1b092-244">Сохраняемость данных Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-244">Redis data persistence</span></span>
<span data-ttu-id="1b092-245">Щелкните **Сохраняемость данных Redis** , чтобы включить, отключить или настроить сохраняемость данных кэша категории «Премиум».</span><span class="sxs-lookup"><span data-stu-id="1b092-245">Click **Redis data persistence** to enable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="1b092-246">Кэш Redis для Azure обеспечивает сохраняемость Redis на основе [RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) или [AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="1b092-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="1b092-247">Дополнительные сведения см. в статье [Настройка постоянного хранения для кэша Redis для Azure уровня Премиум](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-247">For more information, see [How to configure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="1b092-248">Сохраняемость данных Redis доступна только для кэшей категории «Премиум».</span><span class="sxs-lookup"><span data-stu-id="1b092-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="1b092-249">запланировать обновления</span><span class="sxs-lookup"><span data-stu-id="1b092-249">Schedule updates</span></span>
<span data-ttu-id="1b092-250">В колонке **Schedule updates** (Планирование обновлений) можно указать период обслуживания для обновления сервера кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="1b092-250">The **Schedule updates** blade allows you to designate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1b092-251">Данный период обслуживания относится только к обновлениям сервера Redis, а не ко всем обновлениям Azure или операционной системы виртуальных машин, на которых размещен кэш.</span><span class="sxs-lookup"><span data-stu-id="1b092-251">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span></span>
> 
> 

![Планирование обновлений](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="1b092-253">Чтобы задать период обслуживания, отметьте необходимые дни и укажите, когда будет начинаться период обслуживания в каждый из дней, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1b092-253">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="1b092-254">Обратите внимание, что время периода обслуживания указывается в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="1b092-254">Note that the maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1b092-255">Функция **планирования обновлений** доступна только для кэшей категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1b092-255">The **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="1b092-256">Дополнительные сведения и указания см. в разделе о [планировании обновлений](cache-administration.md#schedule-updates) статьи, посвященной администрированию кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="1b092-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="1b092-257">Георепликация</span><span class="sxs-lookup"><span data-stu-id="1b092-257">Geo-replication</span></span>

<span data-ttu-id="1b092-258">Колонка **Георепликация** предоставляет механизм связывания двух экземпляров кэша Redis для Azure категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1b092-258">The **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="1b092-259">Один кэш используется в качестве основного связанного кэша, а другой — как дополнительный связанный кэш.</span><span class="sxs-lookup"><span data-stu-id="1b092-259">One cache is designated as the primary linked cache, and the other as the secondary linked cache.</span></span> <span data-ttu-id="1b092-260">Дополнительный связанный кэш становится доступным только для чтения, и в него реплицируются данные, записанные в основной кэш.</span><span class="sxs-lookup"><span data-stu-id="1b092-260">The secondary linked cache becomes read-only, and data written to the primary cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="1b092-261">Эту функцию можно использовать для репликации кэша в разные регионы Azure.</span><span class="sxs-lookup"><span data-stu-id="1b092-261">This functionality can be used to replicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b092-262">**Георепликация** доступна только для кэшей категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1b092-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="1b092-263">Дополнительные сведения и инструкции см. в статье [How to configure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md) (Как настроить георепликацию для кэша Redis для Azure).</span><span class="sxs-lookup"><span data-stu-id="1b092-263">For more information and instructions, see [How to configure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="1b092-264">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="1b092-264">Virtual Network</span></span>
<span data-ttu-id="1b092-265">В разделе **Виртуальная сеть** можно настроить параметры виртуальной сети для кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-265">The **Virtual Network** section allows you to configure the virtual network settings for your cache.</span></span> <span data-ttu-id="1b092-266">Дополнительные сведения о создании кэша уровня Премиум с поддержкой виртуальной сети и обновлении ее параметров см. в статье [Настройка поддержки виртуальной сети для кэша Redis для Azure уровня Премиум](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-266">For information on creating a premium cache with VNET support and updating its settings, see [How to configure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b092-267">Параметры виртуальной сети доступны только для кэшей уровня Премиум, которые были настроены с поддержкой виртуальной сети во время создания кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="1b092-268">Брандмауэр</span><span class="sxs-lookup"><span data-stu-id="1b092-268">Firewall</span></span>

<span data-ttu-id="1b092-269">Щелкните **Брандмауэр**, чтобы просмотреть и настроить правила брандмауэра для кэша Redis для Azure уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1b092-269">Click **Firewall** to view and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Брандмауэр](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="1b092-271">В правилах брандмауэра можно указать начало и конец диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1b092-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="1b092-272">Когда правила брандмауэра будут настроены, подключения к кэшу будут доступны только для клиентов из указанного диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1b092-272">When firewall rules are configured, only client connections from the specified IP address ranges can connect to the cache.</span></span> <span data-ttu-id="1b092-273">После сохранения правила брандмауэра существует небольшая задержка, прежде чем правило начинает действовать.</span><span class="sxs-lookup"><span data-stu-id="1b092-273">When a firewall rule is saved there is a short delay before the rule is effective.</span></span> <span data-ttu-id="1b092-274">Обычно эта задержка не длится более одной минуты.</span><span class="sxs-lookup"><span data-stu-id="1b092-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b092-275">Подключения из систем мониторинга кэша Redis для Azure всегда разрешены, даже если настроены правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="1b092-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="1b092-276">Правила брандмауэра доступны только для кэшей уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1b092-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="1b092-277">Свойства</span><span class="sxs-lookup"><span data-stu-id="1b092-277">Properties</span></span>
<span data-ttu-id="1b092-278">Щелкните **Свойства** , чтобы отобразить сведения о кэше, включая конечную точку и порты кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-278">Click **Properties** to view information about your cache, including the cache endpoint and ports.</span></span>

![Свойства кэша Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="1b092-280">Блокировки</span><span class="sxs-lookup"><span data-stu-id="1b092-280">Locks</span></span>
<span data-ttu-id="1b092-281">Раздел **Блокировки** позволяет заблокировать подписку, ресурс или группу ресурсов, чтобы другие пользователи в организации не могли случайно удалить или изменить критически важные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1b092-281">The **Locks** section allows you to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="1b092-282">Дополнительные сведения см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="1b092-283">Сценарий автоматизации</span><span class="sxs-lookup"><span data-stu-id="1b092-283">Automation script</span></span>

<span data-ttu-id="1b092-284">Щелкните **Сценарий автоматизации**, чтобы создать и экспортировать шаблон развернутых ресурсов для использования в будущих развертываниях.</span><span class="sxs-lookup"><span data-stu-id="1b092-284">Click **Automation script** to build and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="1b092-285">Дополнительные сведения о работе с шаблонами см. в статье [Развертывание ресурсов с использованием шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="1b092-286">Параметры администрирования</span><span class="sxs-lookup"><span data-stu-id="1b092-286">Administration settings</span></span>
<span data-ttu-id="1b092-287">Параметры в разделе **Администрирование** позволяют выполнить следующие задачи администрирования для кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-287">The settings in the **Administration** section allow you to perform the following administrative tasks for your cache.</span></span> 

![Администрирование](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="1b092-289">Импорт данных</span><span class="sxs-lookup"><span data-stu-id="1b092-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="1b092-290">Экспорт данных</span><span class="sxs-lookup"><span data-stu-id="1b092-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="1b092-291">Reboot</span><span class="sxs-lookup"><span data-stu-id="1b092-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="1b092-292">Импорт и экспорт</span><span class="sxs-lookup"><span data-stu-id="1b092-292">Import/Export</span></span>
<span data-ttu-id="1b092-293">Функция импорта/экспорта является операцией управления данными в кэше Redis для Azure, которая позволяет импортировать данные в кэш и экспортировать их оттуда путем импорта и экспорта моментального снимка базы данных кэша Redis (RDB) из кэша уровня "Премиум" в страничный BLOB-объект в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="1b092-293">Import/Export is an Azure Redis Cache data management operation, which allows you to import and export data in the cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a page blob in an Azure Storage Account.</span></span> <span data-ttu-id="1b092-294">Функция импорта/экспорта дает возможность переключаться между различными экземплярами кэша Redis для Azure или заполнять кэш данными перед использованием.</span><span class="sxs-lookup"><span data-stu-id="1b092-294">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="1b092-295">Импорт можно использовать для переноса RDB-файлов, совместимых с Redis, с сервера Redis, запущенного в любом облаке или любой среде, включая Redis в Linux, Windows, или у любого поставщика облачных служб, такого как Amazon Web Services или другого.</span><span class="sxs-lookup"><span data-stu-id="1b092-295">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="1b092-296">Импорт данных позволяет легко создать кэш, предварительно заполненный данными.</span><span class="sxs-lookup"><span data-stu-id="1b092-296">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="1b092-297">Во время импорта кэш Redis для Azure загружает RDB-файлы из службы хранилища Azure в память, а затем вставляет в кэш ключи.</span><span class="sxs-lookup"><span data-stu-id="1b092-297">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory, and then inserts the keys into the cache.</span></span>

<span data-ttu-id="1b092-298">Экспорт позволяет экспортировать данные, хранящиеся в кэше Redis для Azure, в RDB-файлы, совместимые с Redis.</span><span class="sxs-lookup"><span data-stu-id="1b092-298">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB files.</span></span> <span data-ttu-id="1b092-299">Эту функцию можно использовать для перемещения данных из одного экземпляра кэша Redis для Azure в другой или на другой сервер Redis.</span><span class="sxs-lookup"><span data-stu-id="1b092-299">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="1b092-300">Во время экспорта на виртуальной машине, где размещается экземпляр сервера кэша Redis для Azure, создается временный файл, который отправляется в заданную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="1b092-300">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="1b092-301">После успешного или неудачного завершения операции экспорта этот временный файл удаляется.</span><span class="sxs-lookup"><span data-stu-id="1b092-301">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b092-302">Функция импорта и экспорта доступна только для кэшей категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="1b092-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="1b092-303">Дополнительные сведения и указания см. в статье [Импорт и экспорт данных в кэше Redis для Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="1b092-304">Reboot</span><span class="sxs-lookup"><span data-stu-id="1b092-304">Reboot</span></span>
<span data-ttu-id="1b092-305">Колонка **Перезагрузка** позволяет перезагрузить узлы кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-305">The **Reboot** blade allows you to reboot the nodes of your cache.</span></span> <span data-ttu-id="1b092-306">Функция перезагрузки дает возможность протестировать приложение на устойчивость в случае сбоя узла кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-306">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="1b092-308">Если у вас кэш уровня "Премиум" с включенной кластеризацией, то вы можете выбрать сегменты кэша для перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="1b092-308">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="1b092-310">Чтобы перезагрузить один или несколько узлов кэша, выберите необходимые узлы и нажмите кнопку **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="1b092-310">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span></span> <span data-ttu-id="1b092-311">Если у вас кэш уровня "Премиум" с включенной кластеризацией, выберите сегменты для перезагрузки и нажмите кнопку **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="1b092-311">If you have a premium cache with clustering enabled, select the shard(s) to reboot and then click **Reboot**.</span></span> <span data-ttu-id="1b092-312">Через несколько минут выбранные узлы перезагрузятся, а еще через несколько минут — возобновят работу.</span><span class="sxs-lookup"><span data-stu-id="1b092-312">After a few minutes, the selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b092-313">Перезагрузка теперь доступна для всех ценовых категорий.</span><span class="sxs-lookup"><span data-stu-id="1b092-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="1b092-314">Дополнительные сведения и указания см. в разделе о [перезагрузке](cache-administration.md#reboot) статьи, посвященной администрированию кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="1b092-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="1b092-315">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="1b092-315">Monitoring</span></span>

<span data-ttu-id="1b092-316">В разделе **Мониторинг** можно настроить диагностику и мониторинг для кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="1b092-316">The **Monitoring** section allows you to configure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="1b092-317">Дополнительные сведения о мониторинге и диагностике кэша Redis для Azure см. в статье [Как отслеживать кэш Redis для Azure](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How to monitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Диагностика](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="1b092-319">Метрики Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="1b092-320">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="1b092-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="1b092-321">Диагностика</span><span class="sxs-lookup"><span data-stu-id="1b092-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="1b092-322">Метрики Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-322">Redis metrics</span></span>
<span data-ttu-id="1b092-323">Щелкните **Метрики Redis**, чтобы [просмотреть метрики](cache-how-to-monitor.md#view-cache-metrics) кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-323">Click **Redis metrics** to [view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="1b092-324">Правила оповещения</span><span class="sxs-lookup"><span data-stu-id="1b092-324">Alert rules</span></span>

<span data-ttu-id="1b092-325">Щелкните **Правила оповещения**, чтобы настроить оповещения на основе метрик кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="1b092-325">Click **Alert rules** to configure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="1b092-326">Дополнительные сведения см. в статье [Как отслеживать кэш Redis для Azure](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="1b092-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="1b092-327">Диагностика</span><span class="sxs-lookup"><span data-stu-id="1b092-327">Diagnostics</span></span>

<span data-ttu-id="1b092-328">По умолчанию в Azure Monitor метрики кэша [хранятся в течение 30 дней](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive), а затем удаляются.</span><span class="sxs-lookup"><span data-stu-id="1b092-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="1b092-329">Чтобы сохранить метрики кэша дольше, чем на 30 дней, щелкните **Диагностика**, чтобы [настроить учетную запись хранения](cache-how-to-monitor.md#export-cache-metrics), используемую для хранения диагностических данных кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-329">To persist your cache metrics for longer than 30 days, click **Diagnostics** to [configure the storage account](cache-how-to-monitor.md#export-cache-metrics) used to store cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="1b092-330">В дополнение к архивированию метрик кэша в хранилище вы можете настроить для них [потоковую передачу в концентратор событий или отправку в журнал Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="1b092-330">In addition to archiving your cache metrics to storage, you can also [stream them to an Event hub or send them to Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="1b092-331">Настройки поддержки и устранения неполадок</span><span class="sxs-lookup"><span data-stu-id="1b092-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="1b092-332">Параметры в разделе **Поддержка и устранение неполадок** дают возможности для устранения проблем с кэшем.</span><span class="sxs-lookup"><span data-stu-id="1b092-332">The settings in the **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Поддержка и устранение неполадок](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="1b092-334">Работоспособность ресурса</span><span class="sxs-lookup"><span data-stu-id="1b092-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="1b092-335">Новый запрос в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="1b092-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="1b092-336">Работоспособность ресурса</span><span class="sxs-lookup"><span data-stu-id="1b092-336">Resource health</span></span>
<span data-ttu-id="1b092-337">Служба **работоспособности ресурсов** отслеживает ресурс и сообщает, работает ли он как ожидалось.</span><span class="sxs-lookup"><span data-stu-id="1b092-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="1b092-338">Дополнительные сведения о службе работоспособности ресурсов Azure см. [здесь](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-338">For more information about the Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1b092-339">В настоящее время служба работоспособности ресурсов не поддерживает отправку сведений о работоспособности экземпляров кэша Redis для Azure, размещенных в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="1b092-339">Resource health is currently unable to report on the health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="1b092-340">Дополнительные сведения см. в разделе [Все ли функции кэша работают, когда он размещен в виртуальной сети?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet).</span><span class="sxs-lookup"><span data-stu-id="1b092-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="1b092-341">Новый запрос на техническую поддержку</span><span class="sxs-lookup"><span data-stu-id="1b092-341">New support request</span></span>
<span data-ttu-id="1b092-342">Щелкните **Новый запрос на получение поддержки** , чтобы создать запрос по своему кэшу.</span><span class="sxs-lookup"><span data-stu-id="1b092-342">Click **New support request** to open a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="1b092-343">Конфигурация сервера Redis по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1b092-343">Default Redis server configuration</span></span>
<span data-ttu-id="1b092-344">Новые экземпляры кэша Redis для Azure имеют следующие значения конфигурации Redis по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1b092-344">New Azure Redis Cache instances are configured with the following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="1b092-345">Параметры в этом разделе не удастся изменить с помощью метода `StackExchange.Redis.IServer.ConfigSet`.</span><span class="sxs-lookup"><span data-stu-id="1b092-345">The settings in this section cannot be changed using the `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="1b092-346">При вызове этого метода одной из команд в данном разделе, выдается исключение, аналогичное приведенным ниже:</span><span class="sxs-lookup"><span data-stu-id="1b092-346">If this method is called with one of the commands in this section, an exception similar to the following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="1b092-347">Все настраиваемые значения, такие как **max-memory-policy**, настраиваются на портале Azure или с помощью программ командной строки, таких как Azure CLI или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b092-347">Any values that are configurable, such as **max-memory-policy**, are configurable through the Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="1b092-348">Настройка</span><span class="sxs-lookup"><span data-stu-id="1b092-348">Setting</span></span> | <span data-ttu-id="1b092-349">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1b092-349">Default value</span></span> | <span data-ttu-id="1b092-350">Описание</span><span class="sxs-lookup"><span data-stu-id="1b092-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="1b092-351">16</span><span class="sxs-lookup"><span data-stu-id="1b092-351">16</span></span> |<span data-ttu-id="1b092-352">Количество баз данных по умолчанию — 16. Тем не менее можно указать другое количество в зависимости от ценовой категории<sup>1</sup>. По умолчанию используется база данных DB 0. Вы можете выбрать другую базу данных для отдельных подключений с помощью `connection.GetDatabase(dbid)`, где `dbid` — это число от `0` до `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="1b092-352">The default number of databases is 16 but you can configure a different number based on the pricing tier.<sup>1</sup> The default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="1b092-353">Зависит от ценовой категории.<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="1b092-353">Depends on the pricing tier<sup>2</sup></span></span> |<span data-ttu-id="1b092-354">Это максимально допустимое количество одновременно подключенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="1b092-354">This is the maximum number of connected clients allowed at the same time.</span></span> <span data-ttu-id="1b092-355">После достижения предела Redis закрывает все новые подключения, возвращая сообщение об ошибке "max number of clients reached" (достигнуто максимальное количество клиентов).</span><span class="sxs-lookup"><span data-stu-id="1b092-355">Once the limit is reached Redis closes all the new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="1b092-356">Политика максимальной памяти — это параметр, определяющий то, как Redis выбирает, что следует удалить при достижении `maxmemory` (размера кэша, выбранного вами при создании кэша).</span><span class="sxs-lookup"><span data-stu-id="1b092-356">Maxmemory policy is the setting for how Redis selects what to remove when `maxmemory` (the size of the cache offering you selected when you created the cache) is reached.</span></span> <span data-ttu-id="1b092-357">В случае с кэшем Redis для Azure значением по умолчанию является `volatile-lru`, когда удаляются ключи со сроком действия, устанавливаемым посредством алгоритма LRU.</span><span class="sxs-lookup"><span data-stu-id="1b092-357">With Azure Redis Cache the default setting is `volatile-lru`, which removes the keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="1b092-358">Этот параметр можно настроить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="1b092-358">This setting can be configured in the Azure portal.</span></span> <span data-ttu-id="1b092-359">Дополнительные сведения см. в разделе [Политики памяти](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="1b092-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="1b092-360">3</span><span class="sxs-lookup"><span data-stu-id="1b092-360">3</span></span> |<span data-ttu-id="1b092-361">Для экономии памяти алгоритмы LRU и минимальный TTL являются не точными, а аппроксимированными алгоритмами.</span><span class="sxs-lookup"><span data-stu-id="1b092-361">To save memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="1b092-362">По умолчанию Redis проверяет три ключа и выбирает один, использовавшийся наиболее давно.</span><span class="sxs-lookup"><span data-stu-id="1b092-362">By default Redis checks three keys and picks the one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="1b092-363">5 000</span><span class="sxs-lookup"><span data-stu-id="1b092-363">5,000</span></span> |<span data-ttu-id="1b092-364">Максимальное время выполнения сценария Lua в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="1b092-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="1b092-365">При достижении максимального времени выполнения Redis делает запись в журнале о нахождении данного сценария в процессе выполнения по истечении максимально допустимого времени и начинает отвечать на запросы ошибкой.</span><span class="sxs-lookup"><span data-stu-id="1b092-365">If the maximum execution time is reached, Redis logs that a script is still in execution after the maximum allowed time, and starts to reply to queries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="1b092-366">500</span><span class="sxs-lookup"><span data-stu-id="1b092-366">500</span></span> |<span data-ttu-id="1b092-367">Максимальный размер очереди событий сценариев.</span><span class="sxs-lookup"><span data-stu-id="1b092-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="1b092-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="1b092-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="1b092-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="1b092-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="1b092-370">Ограничения буферов вывода клиентов можно использовать для принудительного отключения клиентов, по каким-либо причинам недостаточно быстро считывающим данные с сервера (распространенной причиной является неспособность клиента Pub/Sub поглощать сообщения так же быстро, как их производит издатель).</span><span class="sxs-lookup"><span data-stu-id="1b092-370">The client output buffer limits can be used to force disconnection of clients that are not reading data from the server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as the publisher can produce them).</span></span> <span data-ttu-id="1b092-371">Дополнительные сведения см. по ссылке [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="1b092-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="1b092-372"><a name="databases"></a>
<sup>1</sup> Для различных ценовых категорий кэша Redis для Azure предельное значение `databases` будет разным. Его можно указать при создании кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-372"><a name="databases"></a>
<sup>1</sup>The limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="1b092-373">Если при создании кэша значение `databases` не указано, то используется значение по умолчанию — 16.</span><span class="sxs-lookup"><span data-stu-id="1b092-373">If no `databases` setting is specified during cache creation, the default is 16.</span></span>

* <span data-ttu-id="1b092-374">Кэши уровней Basic и Standard</span><span class="sxs-lookup"><span data-stu-id="1b092-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="1b092-375">кэш C0 (250 МБ) — до 16 баз данных;</span><span class="sxs-lookup"><span data-stu-id="1b092-375">C0 (250 MB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="1b092-376">кэш C1 (1 ГБ) — до 16 баз данных;</span><span class="sxs-lookup"><span data-stu-id="1b092-376">C1 (1 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="1b092-377">кэш C2 (2,5 ГБ) — до 16 баз данных;</span><span class="sxs-lookup"><span data-stu-id="1b092-377">C2 (2.5 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="1b092-378">кэш C3 (6 ГБ) — до 16 баз данных;</span><span class="sxs-lookup"><span data-stu-id="1b092-378">C3 (6 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="1b092-379">кэш C4 (13 ГБ) — до 32 баз данных;</span><span class="sxs-lookup"><span data-stu-id="1b092-379">C4 (13 GB) cache - up to 32 databases</span></span>
  * <span data-ttu-id="1b092-380">кэш C5 (26 ГБ) — до 48 баз данных;</span><span class="sxs-lookup"><span data-stu-id="1b092-380">C5 (26 GB) cache - up to 48 databases</span></span>
  * <span data-ttu-id="1b092-381">кэш C6 (53 ГБ) — до 64 баз данных.</span><span class="sxs-lookup"><span data-stu-id="1b092-381">C6 (53 GB) cache - up to 64 databases</span></span>
* <span data-ttu-id="1b092-382">Кэши уровня Premium</span><span class="sxs-lookup"><span data-stu-id="1b092-382">Premium caches</span></span>
  * <span data-ttu-id="1b092-383">кэш P1 (6–60 ГБ) — до 16 баз данных;</span><span class="sxs-lookup"><span data-stu-id="1b092-383">P1 (6 GB - 60 GB) - up to 16 databases</span></span>
  * <span data-ttu-id="1b092-384">кэш P2 (13–130 ГБ) — до 32 баз данных;</span><span class="sxs-lookup"><span data-stu-id="1b092-384">P2 (13 GB - 130 GB) - up to 32 databases</span></span>
  * <span data-ttu-id="1b092-385">кэш P3 (26–260 ГБ) — до 48 баз данных;</span><span class="sxs-lookup"><span data-stu-id="1b092-385">P3 (26 GB - 260 GB) - up to 48 databases</span></span>
  * <span data-ttu-id="1b092-386">кэш P4 (53–530 ГБ) — до 64 баз данных.</span><span class="sxs-lookup"><span data-stu-id="1b092-386">P4 (53 GB - 530 GB) - up to 64 databases</span></span>
  * <span data-ttu-id="1b092-387">Для всех кэшей уровня Премиум включен кластер Redis. Он поддерживает только базу данных 0, поэтому предельное значение `databases` для любого кэша уровня Премиум с включенным кластером Redis равно 1, а использование команды [Select](http://redis.io/commands/select) не допускается.</span><span class="sxs-lookup"><span data-stu-id="1b092-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so the `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and the [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="1b092-388">Дополнительные сведения см. в разделе [Нужно ли вносить изменения в клиентское приложение, чтобы использовать кластеризацию?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering).</span><span class="sxs-lookup"><span data-stu-id="1b092-388">For more information, see [Do I need to make any changes to my client application to use clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="1b092-389">Дополнительные сведения о базах данных см. в разделе [Что такое базы данных Redis?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="1b092-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="1b092-390">Параметр `databases` можно настроить только во время создания кэша и только с помощью PowerShell, интерфейса командной строки или других клиентов управления.</span><span class="sxs-lookup"><span data-stu-id="1b092-390">The `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="1b092-391">Пример настройки `databases` во время создания кэша с помощью PowerShell см. в разделе о командлете [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="1b092-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="1b092-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` отличается для каждой ценовой категории кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="1b092-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="1b092-393">Кэши уровней Basic и Standard</span><span class="sxs-lookup"><span data-stu-id="1b092-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="1b092-394">кэш C0 (250 МБ) — до 256 подключений;</span><span class="sxs-lookup"><span data-stu-id="1b092-394">C0 (250 MB) cache - up to 256 connections</span></span>
  * <span data-ttu-id="1b092-395">кэш C1 (1 ГБ) — до 1000 подключений;</span><span class="sxs-lookup"><span data-stu-id="1b092-395">C1 (1 GB) cache - up to 1,000 connections</span></span>
  * <span data-ttu-id="1b092-396">кэш C2 (2.5 ГБ) — до 2000 подключений;</span><span class="sxs-lookup"><span data-stu-id="1b092-396">C2 (2.5 GB) cache - up to 2,000 connections</span></span>
  * <span data-ttu-id="1b092-397">кэш C3 (6 ГБ) — до 5000 подключений;</span><span class="sxs-lookup"><span data-stu-id="1b092-397">C3 (6 GB) cache - up to 5,000 connections</span></span>
  * <span data-ttu-id="1b092-398">кэш C4 (13 ГБ) — до 10 000 подключений;</span><span class="sxs-lookup"><span data-stu-id="1b092-398">C4 (13 GB) cache - up to 10,000 connections</span></span>
  * <span data-ttu-id="1b092-399">кэш C5 (26 ГБ) — до 15 000 подключений;</span><span class="sxs-lookup"><span data-stu-id="1b092-399">C5 (26 GB) cache - up to 15,000 connections</span></span>
  * <span data-ttu-id="1b092-400">кэш C6 (53 ГБ) — до 20 000 подключений.</span><span class="sxs-lookup"><span data-stu-id="1b092-400">C6 (53 GB) cache - up to 20,000 connections</span></span>
* <span data-ttu-id="1b092-401">Кэши уровня Premium</span><span class="sxs-lookup"><span data-stu-id="1b092-401">Premium caches</span></span>
  * <span data-ttu-id="1b092-402">P1 (6–60 ГБ): до 7500 подключений</span><span class="sxs-lookup"><span data-stu-id="1b092-402">P1 (6 GB - 60 GB) - up to 7,500 connections</span></span>
  * <span data-ttu-id="1b092-403">P2 (13–130 ГБ): до 15 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1b092-403">P2 (13 GB - 130 GB) - up to 15,000 connections</span></span>
  * <span data-ttu-id="1b092-404">P3 (26–260 ГБ): до 30 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1b092-404">P3 (26 GB - 260 GB) - up to 30,000 connections</span></span>
  * <span data-ttu-id="1b092-405">P4 (53–530 ГБ): до 40 000 подключений</span><span class="sxs-lookup"><span data-stu-id="1b092-405">P4 (53 GB - 530 GB) - up to 40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="1b092-406">Хотя каждый размер кэша *допускает* определенное число подключений, с каждым подключением к Redis связаны накладные расходы.</span><span class="sxs-lookup"><span data-stu-id="1b092-406">While each size of cache allows *up to* a certain number of connections, each connection to Redis has overhead associated with it.</span></span> <span data-ttu-id="1b092-407">Примером таких накладных расходов могут служить загрузка ЦП и использование памяти в результате шифрования TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="1b092-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="1b092-408">Максимальное число подключений для данного размера кэша предполагает низкую загрузку кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-408">The maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="1b092-409">Если *суммарная* нагрузка, связанная с подключениями и клиентскими операциями, превышает емкость системы, могут возникнуть проблемы с работой кэша, даже если максимальное число подключений для его текущего размера не превышено.</span><span class="sxs-lookup"><span data-stu-id="1b092-409">If load from connection overhead *plus* load from client operations exceeds capacity for the system, the cache can experience capacity issues even if you have not exceeded the connection limit for the current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="1b092-410">Команды Redis не поддерживаются в кэше Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="1b092-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1b092-411">Поскольку настройка и управление экземплярами кэша Redis для Azure осуществляется Майкрософт, следующие команды отключены.</span><span class="sxs-lookup"><span data-stu-id="1b092-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, the following commands are disabled.</span></span> <span data-ttu-id="1b092-412">При попытке их вызвать появляется сообщение об ошибке примерно следующего содержания: `"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="1b092-412">If you try to invoke them, you receive an error message similar to `"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="1b092-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="1b092-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="1b092-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="1b092-414">BGSAVE</span></span>
> * <span data-ttu-id="1b092-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="1b092-415">CONFIG</span></span>
> * <span data-ttu-id="1b092-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="1b092-416">DEBUG</span></span>
> * <span data-ttu-id="1b092-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="1b092-417">MIGRATE</span></span>
> * <span data-ttu-id="1b092-418">Сохранить</span><span class="sxs-lookup"><span data-stu-id="1b092-418">SAVE</span></span>
> * <span data-ttu-id="1b092-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="1b092-419">SHUTDOWN</span></span>
> * <span data-ttu-id="1b092-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="1b092-420">SLAVEOF</span></span>
> * <span data-ttu-id="1b092-421">CLUSTER — команды записи для кластера отключены, однако допускается использование кластерных команд только для чтения.</span><span class="sxs-lookup"><span data-stu-id="1b092-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="1b092-422">Дополнительные сведения о командах Redis см. по ссылке [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="1b092-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="1b092-423">Консоль Redis</span><span class="sxs-lookup"><span data-stu-id="1b092-423">Redis console</span></span>
<span data-ttu-id="1b092-424">В экземплярах кэша Redis для Azure можно безопасно выполнять команды с помощью **консоли Redis**, доступной на портале Azure для всех категорий кэшей.</span><span class="sxs-lookup"><span data-stu-id="1b092-424">You can securely issue commands to your Azure Redis Cache instances using the **Redis Console**, which is available in the Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="1b092-425">Консоль Redis не работает с [VNET](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-425">The Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="1b092-426">Если кэш является частью виртуальной сети, то к нему могут обращаться только клиенты в этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="1b092-426">When your cache is part of a VNET, only clients in the VNET can access the cache.</span></span> <span data-ttu-id="1b092-427">Так как консоль Redis работает в локальном браузере вне виртуальной сети, она не может подключиться к кэшу.</span><span class="sxs-lookup"><span data-stu-id="1b092-427">Because Redis Console runs in your local browser, which is outside the VNET, it can't connect to your cache.</span></span>
> - <span data-ttu-id="1b092-428">В кэше Redis для Azure поддерживаются не все команды Redis.</span><span class="sxs-lookup"><span data-stu-id="1b092-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="1b092-429">Список команд Redis, отключенных в кэше Redis для Azure, см. в предыдущем разделе [Команды Redis, не поддерживаемые в кэше Redis для Azure](#redis-commands-not-supported-in-azure-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="1b092-429">For a list of Redis commands that are disabled for Azure Redis Cache, see the previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="1b092-430">Дополнительные сведения о командах Redis см. по ссылке [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="1b092-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="1b092-431">Чтобы иметь доступ к консоли Redis, в колонке **Кэш Redis** щелкните **Консоль**.</span><span class="sxs-lookup"><span data-stu-id="1b092-431">To access the Redis Console, click **Console** from the **Redis Cache** blade.</span></span>

![Консоль Redis](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="1b092-433">Чтобы выполнить команду в своем экземпляре кэша, просто введите нужную команду в консоль.</span><span class="sxs-lookup"><span data-stu-id="1b092-433">To issue commands against your cache instance, simply type the desired command into the console.</span></span>

![Консоль Redis](./media/cache-configure/redis-console.png)


### <a name="using-the-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="1b092-435">Использование консоли Redis с кластеризированным кэшем категории "Премиум"</span><span class="sxs-lookup"><span data-stu-id="1b092-435">Using the Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="1b092-436">При использовании консоли Redis с кластеризированным кэшем категории "Премиум" можно выполнять команды для одного сегмента кэша.</span><span class="sxs-lookup"><span data-stu-id="1b092-436">When using the Redis Console with a premium clustered cache, you can issue commands to a single shard of the cache.</span></span> <span data-ttu-id="1b092-437">Чтобы выполнить команду для конкретного сегмента, сначала подключитесь к нужному сегменту, щелкнув его в окне выбора сегментов.</span><span class="sxs-lookup"><span data-stu-id="1b092-437">To issue a command to a specific shard, first connect to the desired shard by clicking it on the shard picker.</span></span>

![Консоль Redis](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="1b092-439">При попытке получить доступ к ключу, который хранится в другом сегменте, вы получите следующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="1b092-439">If you attempt to access a key that is stored in a different shard than the connected shard, you receive an error message similar to the following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="1b092-440">В предыдущем примере выбран сегмент 1, но `myKey` находится в сегменте 0, как указано в части `(shard 0)` сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="1b092-440">In the previous example, shard 1 is the selected shard, but `myKey` is located in shard 0, as indicated by the `(shard 0)` portion of the error message.</span></span> <span data-ttu-id="1b092-441">В этом примере для доступа к `myKey` выберите сегмент 0 с помощью средства выбора сегментов, а затем выполните необходимую команду.</span><span class="sxs-lookup"><span data-stu-id="1b092-441">In this example, to access `myKey`, select shard 0 using the shard picker, and then issue the desired command.</span></span>


## <a name="move-your-cache-to-a-new-subscription"></a><span data-ttu-id="1b092-442">Перемещение кэша в новую подписку</span><span class="sxs-lookup"><span data-stu-id="1b092-442">Move your cache to a new subscription</span></span>
<span data-ttu-id="1b092-443">Для перемещения кэша в новую подписку щелкните **Переместить**.</span><span class="sxs-lookup"><span data-stu-id="1b092-443">You can move your cache to a new subscription by clicking **Move**.</span></span>

![Перемещение кэша Redis](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="1b092-445">Сведения о перемещении ресурсов из одной группы ресурсов в другую, а также из одной подписки в другую см. в статье [Перемещение ресурсов в новую группу ресурсов или подписку](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="1b092-445">For information on moving resources from one resource group to another, and from one subscription to another, see [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b092-446">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b092-446">Next steps</span></span>
* <span data-ttu-id="1b092-447">Дополнительные сведения о работе с командами Redis см. в разделе [Как выполнять команды Redis?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="1b092-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

