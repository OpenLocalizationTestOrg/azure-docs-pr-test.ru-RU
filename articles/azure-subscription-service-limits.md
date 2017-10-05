---
title: "Ограничения и квоты подписки Azure | Документация Майкрософт"
description: "В этой статье приводится перечень наиболее распространенных ограничений, относящихся к подписке Azure и различным службам, квот и границ. Сюда входит информация о том, как увеличить лимиты и максимальные значения."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a76acd67e9ba7822f2837b3c08e2ede389047f11
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="b120d-104">Подписка Azure, границы, квоты и ограничения службы</span><span class="sxs-lookup"><span data-stu-id="b120d-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="b120d-105">В этом документе указаны некоторые из наиболее распространенных ограничений Microsoft Azure, которые иногда называются квотами.</span><span class="sxs-lookup"><span data-stu-id="b120d-105">This document lists some of the most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="b120d-106">Этот документ на текущий момент охватывает не все службы Azure.</span><span class="sxs-lookup"><span data-stu-id="b120d-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="b120d-107">Со временем список будет расширен и обновлен, чтобы охватить больше платформ.</span><span class="sxs-lookup"><span data-stu-id="b120d-107">Over time, the list will be expanded and updated to cover more of the platform.</span></span>

<span data-ttu-id="b120d-108">Дополнительную информацию о ценах Azure см. на странице [Цены Azure](https://azure.microsoft.com/pricing/).</span><span class="sxs-lookup"><span data-stu-id="b120d-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) to learn more about Azure pricing.</span></span> <span data-ttu-id="b120d-109">Там вы сможете оценить затраты с помощью [калькулятора цен](https://azure.microsoft.com/pricing/calculator/) или просмотрев страницу сведений о ценах для службы (например, для [виртуальных машин Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="b120d-109">There, you can estimate your costs using the [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting the pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="b120d-110">Советы по управлению затратами приведены в статье [Предотвращение непредвиденных расходов с помощью функции выставления счетов и управления затратами в Azure](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b120d-110">For tips to help manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b120d-111">Если ограничение или квоту требуется сделать выше значения **Ограничение по умолчанию**, [бесплатно отправьте запрос в службу поддержки клиентов](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="b120d-111">If you want to raise the limit or quota above the **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="b120d-112">Ограничения не могут быть увеличены выше значения **Максимальное ограничение**, как показано в таблицах ниже.</span><span class="sxs-lookup"><span data-stu-id="b120d-112">The limits can't be raised above the **Maximum Limit** value shown in the following tables.</span></span> <span data-ttu-id="b120d-113">Если столбца **Максимальное ограничение** нет, то ресурс не имеет настраиваемого ограничения.</span><span class="sxs-lookup"><span data-stu-id="b120d-113">If there is no **Maximum Limit** column, then the resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="b120d-114">Бесплатная пробная версия подписки не предусматривает возможность увеличения ограничения и квоты.</span><span class="sxs-lookup"><span data-stu-id="b120d-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="b120d-115">При наличии бесплатной пробной подписки ее можно обновить до подписки [с оплатой по мере использования](https://azure.microsoft.com/offers/ms-azr-0003p/).</span><span class="sxs-lookup"><span data-stu-id="b120d-115">If you have a Free Trial, you can upgrade to a [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="b120d-116">Дополнительные сведения см. в статье [Upgrade your free Azure subscription to Pay-As-You-Go](billing/billing-upgrade-azure-subscription.md) (Обновление бесплатной пробной версии Azure до версии с оплатой по мере использования).</span><span class="sxs-lookup"><span data-stu-id="b120d-116">For more information, see [Upgrade Azure Free Trial to Pay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-the-azure-resource-manager"></a><span data-ttu-id="b120d-117">Ограничения и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b120d-117">Limits and the Azure Resource Manager</span></span>
<span data-ttu-id="b120d-118">Теперь несколько ресурсов можно объединить в одной группе ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b120d-118">It is now possible to combine multiple Azure resources in to a single Azure Resource Group.</span></span> <span data-ttu-id="b120d-119">При использовании групп ресурсов ограничения, которые были глобальными, становятся управляемыми на региональном уровне благодаря диспетчеру ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b120d-119">When using Resource Groups, limits that once were global become managed at a regional level with the Azure Resource Manager.</span></span> <span data-ttu-id="b120d-120">Дополнительные сведения о группах ресурсов Azure см. в статье [Общие сведения о диспетчере ресурсов Azure](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b120d-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b120d-121">В следующие ограничения добавлена новая таблица, в которой отражены все различия ограничений при использовании диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b120d-121">In the limits below, a new table has been added to reflect any differences in limits when using the Azure Resource Manager.</span></span> <span data-ttu-id="b120d-122">Например, имеется таблица **Ограничения подписки** и таблица **Ограничения подписки — Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="b120d-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="b120d-123">Если ограничение применяется в обоих случаях, оно показано только в первой таблице.</span><span class="sxs-lookup"><span data-stu-id="b120d-123">When a limit applies to both scenarios, it is only shown in the first table.</span></span> <span data-ttu-id="b120d-124">Если не указано иное, ограничения глобальны во всех областях.</span><span class="sxs-lookup"><span data-stu-id="b120d-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="b120d-125">Важно подчеркнуть, что квоты для ресурсов в группах ресурсов Azure доступны для каждого региона по подписке, а не для каждой подписки, как квоты управления службами.</span><span class="sxs-lookup"><span data-stu-id="b120d-125">It is important to emphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as the service management quotas are.</span></span> <span data-ttu-id="b120d-126">В качестве примера используем квоты ядер ЦП.</span><span class="sxs-lookup"><span data-stu-id="b120d-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="b120d-127">Если вам необходимо запросить увеличение квоты с поддержкой ядер, следует решить, сколько ядер будут использоваться и в каких регионах, а затем отправить запрос на квоты ядер группы ресурсов Azure core с нужными регионами и количеством.</span><span class="sxs-lookup"><span data-stu-id="b120d-127">If you need to request a quota increase with support for cores, you need to decide how many cores you want to use in which regions, and then make a specific request for Azure Resource Group core quotas for the amounts and regions that you want.</span></span> <span data-ttu-id="b120d-128">Поэтому, если необходимо использовать 30 ядер в Западной Европе для запуска приложения, следует запросить 30 ядер в Западной Европе.</span><span class="sxs-lookup"><span data-stu-id="b120d-128">Therefore, if you need to use 30 cores in West Europe to run your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="b120d-129">Но других регионах квота ядер не увеличится не будет — только в Западной Европе будет 30 ядер.</span><span class="sxs-lookup"><span data-stu-id="b120d-129">But you will not have a core quota increase in any other region -- only West Europe will have the 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="b120d-130">В результате может быть полезно проанализировать, какие квоты группы ресурсов Azure потребуется для вашей рабочей нагрузки в каждом регионе, и запросить эти ресурсы в регионах, где выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="b120d-130">As a result, you may find it useful to consider deciding what your Azure Resource Group quotas need to be for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="b120d-131">Подробные сведения об определении текущих квот для конкретных регионов см. в разделе [Устранение неполадок развертывания](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="b120d-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="b120d-132">Ограничения определенных служб</span><span class="sxs-lookup"><span data-stu-id="b120d-132">Service-specific limits</span></span>
* [<span data-ttu-id="b120d-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="b120d-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="b120d-134">Управление API</span><span class="sxs-lookup"><span data-stu-id="b120d-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="b120d-135">Служба приложений</span><span class="sxs-lookup"><span data-stu-id="b120d-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="b120d-136">Шлюз приложений</span><span class="sxs-lookup"><span data-stu-id="b120d-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="b120d-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="b120d-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="b120d-138">Автоматизация</span><span class="sxs-lookup"><span data-stu-id="b120d-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="b120d-139">База данных Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="b120d-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="b120d-140">Сетка событий Azure</span><span class="sxs-lookup"><span data-stu-id="b120d-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="b120d-141">кэш Azure Redis</span><span class="sxs-lookup"><span data-stu-id="b120d-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="b120d-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b120d-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="b120d-143">Архивация</span><span class="sxs-lookup"><span data-stu-id="b120d-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="b120d-144">Пакетная служба</span><span class="sxs-lookup"><span data-stu-id="b120d-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="b120d-145">Службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="b120d-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="b120d-146">CDN</span><span class="sxs-lookup"><span data-stu-id="b120d-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="b120d-147">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="b120d-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="b120d-148">Экземпляры контейнеров</span><span class="sxs-lookup"><span data-stu-id="b120d-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="b120d-149">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="b120d-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="b120d-150">Аналитика озера данных</span><span class="sxs-lookup"><span data-stu-id="b120d-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="b120d-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b120d-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="b120d-152">DNS</span><span class="sxs-lookup"><span data-stu-id="b120d-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="b120d-153">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="b120d-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="b120d-154">Центр Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="b120d-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="b120d-155">хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="b120d-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="b120d-156">Log Analytics или Operational Insights</span><span class="sxs-lookup"><span data-stu-id="b120d-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="b120d-157">Службы мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b120d-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="b120d-158">Службы мобильного взаимодействия;</span><span class="sxs-lookup"><span data-stu-id="b120d-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="b120d-159">Мобильные службы</span><span class="sxs-lookup"><span data-stu-id="b120d-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="b120d-160">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="b120d-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="b120d-161">Многофакторная идентификация</span><span class="sxs-lookup"><span data-stu-id="b120d-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="b120d-162">Сеть</span><span class="sxs-lookup"><span data-stu-id="b120d-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="b120d-163">Наблюдатель за сетями</span><span class="sxs-lookup"><span data-stu-id="b120d-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="b120d-164">Служба концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="b120d-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="b120d-165">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="b120d-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="b120d-166">Планировщик</span><span class="sxs-lookup"><span data-stu-id="b120d-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="b120d-167">Поиск</span><span class="sxs-lookup"><span data-stu-id="b120d-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="b120d-168">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="b120d-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="b120d-169">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b120d-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="b120d-170">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="b120d-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="b120d-171">Хранилище</span><span class="sxs-lookup"><span data-stu-id="b120d-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="b120d-172">StorSimple System</span><span class="sxs-lookup"><span data-stu-id="b120d-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="b120d-173">Анализ потока</span><span class="sxs-lookup"><span data-stu-id="b120d-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="b120d-174">Подписка</span><span class="sxs-lookup"><span data-stu-id="b120d-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="b120d-175">Диспетчер трафика</span><span class="sxs-lookup"><span data-stu-id="b120d-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="b120d-176">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="b120d-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="b120d-177">Наборы для масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="b120d-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="b120d-178">Ограничения подписки</span><span class="sxs-lookup"><span data-stu-id="b120d-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="b120d-179">Ограничения подписки</span><span class="sxs-lookup"><span data-stu-id="b120d-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="b120d-180">Ограничения подписки — Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b120d-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="b120d-181">При использовании диспетчера ресурсов Azure и групп ресурсов Azure применяются следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="b120d-181">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="b120d-182">Ограничения, которые не были изменены после выпуска диспетчера ресурсов Azure, ниже не перечислены.</span><span class="sxs-lookup"><span data-stu-id="b120d-182">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="b120d-183">Их можно просмотреть в предыдущей таблице.</span><span class="sxs-lookup"><span data-stu-id="b120d-183">Please refer to the previous table for those limits.</span></span>

<span data-ttu-id="b120d-184">Сведения о работе с ограничениями на запросы Resource Manager см. в разделе [Throttling Resource Manager requests](resource-manager-request-limits.md) (Регулирование запросов Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="b120d-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="b120d-185">Ограничения группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="b120d-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="b120d-186">Ограничения виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="b120d-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="b120d-187">Ограничения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b120d-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="b120d-188">Ограничения виртуальных машин — диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b120d-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="b120d-189">При использовании диспетчера ресурсов Azure и групп ресурсов Azure применяются следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="b120d-189">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="b120d-190">Ограничения, которые не были изменены после выпуска диспетчера ресурсов Azure, ниже не перечислены.</span><span class="sxs-lookup"><span data-stu-id="b120d-190">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="b120d-191">Их можно просмотреть в предыдущей таблице.</span><span class="sxs-lookup"><span data-stu-id="b120d-191">Please refer to the previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="b120d-192">Ограничения для масштабируемых наборов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="b120d-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="b120d-193">Ограничения для экземпляров контейнеров</span><span class="sxs-lookup"><span data-stu-id="b120d-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="b120d-194">Ограничения сети</span><span class="sxs-lookup"><span data-stu-id="b120d-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="b120d-195">Ограничения сети</span><span class="sxs-lookup"><span data-stu-id="b120d-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="b120d-196">Ограничения шлюза приложений</span><span class="sxs-lookup"><span data-stu-id="b120d-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="b120d-197">Пределы наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="b120d-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="b120d-198">Ограничения диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="b120d-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="b120d-199">Ограничения DNS</span><span class="sxs-lookup"><span data-stu-id="b120d-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="b120d-200">Ограничения хранилища</span><span class="sxs-lookup"><span data-stu-id="b120d-200">Storage limits</span></span>
<span data-ttu-id="b120d-201">Дополнительные сведения об ограничениях учетных записей хранения см. в статье [Целевые показатели по производительности и масштабируемости для хранилища Azure](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="b120d-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="b120d-202">Ограничения службы хранения</span><span class="sxs-lookup"><span data-stu-id="b120d-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="b120d-203">Ограничения для дисков виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b120d-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="b120d-204">Дополнительные сведения см. в статье [Размеры виртуальных машин](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b120d-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="b120d-205">Управляемые диски виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b120d-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="b120d-206">Неуправляемые диски виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b120d-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="b120d-207">Ограничения поставщика ресурсов хранилища</span><span class="sxs-lookup"><span data-stu-id="b120d-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="b120d-208">Ограничения облачных служб</span><span class="sxs-lookup"><span data-stu-id="b120d-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="b120d-209">Ограничения службы приложений</span><span class="sxs-lookup"><span data-stu-id="b120d-209">App Service limits</span></span>
<span data-ttu-id="b120d-210">Следующие ограничения службы приложения включают ограничения для веб-приложений, мобильных приложений, приложений API и приложений логики.</span><span class="sxs-lookup"><span data-stu-id="b120d-210">The following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="b120d-211">Ограничения планировщика</span><span class="sxs-lookup"><span data-stu-id="b120d-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="b120d-212">Ограничения пакета</span><span class="sxs-lookup"><span data-stu-id="b120d-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="b120d-213">Ограничения служб BizTalk</span><span class="sxs-lookup"><span data-stu-id="b120d-213">BizTalk Services limits</span></span>
<span data-ttu-id="b120d-214">В следующей таблице показаны ограничения для служб BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="b120d-214">The following table shows the limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="b120d-215">Ограничения Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b120d-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="b120d-216">Azure Cosmos DB — это глобальная база данных, пропускную способность и хранилище которой можно масштабировать в соответствии с требованиями приложения.</span><span class="sxs-lookup"><span data-stu-id="b120d-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled to handle whatever your application requires.</span></span> <span data-ttu-id="b120d-217">Если у вас возникнут вопросы по масштабированию Azure Cosmos DB, отправьте электронное сообщение по адресу askcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="b120d-217">If you have any questions about the scale Azure Cosmos DB provides, please send email to askcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="b120d-218">Ограничения Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="b120d-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="b120d-219">Ограничения поиска</span><span class="sxs-lookup"><span data-stu-id="b120d-219">Search limits</span></span>
<span data-ttu-id="b120d-220">Ценовые категории определяют емкость и ограничения службы поиска.</span><span class="sxs-lookup"><span data-stu-id="b120d-220">Pricing tiers determine the capacity and limits of your search service.</span></span> <span data-ttu-id="b120d-221">Существуют следующие категории:</span><span class="sxs-lookup"><span data-stu-id="b120d-221">Tiers include:</span></span>

* <span data-ttu-id="b120d-222">*Бесплатный* : мультитенантная служба, используемая совместно с другими подписчиками Azure и предназначенная для оценки и разработки небольших проектов.</span><span class="sxs-lookup"><span data-stu-id="b120d-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="b120d-223">*Базовый* предоставляет выделенные вычислительные ресурсы для небольших рабочих нагрузок в рабочей среде, поддерживая до трех реплик для обработки запросов с высоким уровнем доступности.</span><span class="sxs-lookup"><span data-stu-id="b120d-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up to three replicas for highly available query workloads.</span></span>
* <span data-ttu-id="b120d-224">*Стандартный (S1, S2, S3, S3 с высокой плотностью)* предназначена для больших рабочих нагрузок в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b120d-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="b120d-225">В рамках уровня "Стандартный" есть несколько уровней, поэтому можно выбрать конфигурацию ресурсов, которая лучше всего подходит для вашего профиля рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b120d-225">Multiple levels exist within the standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="b120d-226">**Ограничения на одну подписку**</span><span class="sxs-lookup"><span data-stu-id="b120d-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="b120d-227">**Ограничения на одну службу поиска**</span><span class="sxs-lookup"><span data-stu-id="b120d-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="b120d-228">Дополнительные сведения об ограничениях, включая размер документов, количество запросов в секунду, ключи, запросы и ответы, см. в статье [Ограничения поиска Azure](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="b120d-228">To learn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="b120d-229">Ограничения служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b120d-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="b120d-230">Ограничения CDN</span><span class="sxs-lookup"><span data-stu-id="b120d-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="b120d-231">Ограничения мобильных служб</span><span class="sxs-lookup"><span data-stu-id="b120d-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="b120d-232">Пределы монитора</span><span class="sxs-lookup"><span data-stu-id="b120d-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="b120d-233">Ограничения служб концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="b120d-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="b120d-234">Ограничения концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="b120d-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="b120d-235">Ограничения служебной шины</span><span class="sxs-lookup"><span data-stu-id="b120d-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="b120d-236">Пределы для Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="b120d-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="b120d-237">Ограничения фабрики данных</span><span class="sxs-lookup"><span data-stu-id="b120d-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="b120d-238">Ограничения Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b120d-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="b120d-239">Ограничения Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b120d-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="b120d-240">Ограничения Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b120d-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="b120d-241">Ограничения Active Directory</span><span class="sxs-lookup"><span data-stu-id="b120d-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="b120d-242">Ограничения сетки событий Azure</span><span class="sxs-lookup"><span data-stu-id="b120d-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="b120d-243">Ограничения Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b120d-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="b120d-244">Ограничения системы StorSimple</span><span class="sxs-lookup"><span data-stu-id="b120d-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="b120d-245">Ограничения Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b120d-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="b120d-246">Ограничения резервного копирования</span><span class="sxs-lookup"><span data-stu-id="b120d-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="b120d-247">Ограничения Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b120d-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="b120d-248">Ограничения Application Insights</span><span class="sxs-lookup"><span data-stu-id="b120d-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="b120d-249">Ограничения управления API</span><span class="sxs-lookup"><span data-stu-id="b120d-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="b120d-250">Ограничения кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="b120d-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="b120d-251">Ограничения хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="b120d-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="b120d-252">Многофакторная идентификация</span><span class="sxs-lookup"><span data-stu-id="b120d-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="b120d-253">Ограничения автоматизации</span><span class="sxs-lookup"><span data-stu-id="b120d-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="b120d-254">Ограничения базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="b120d-254">SQL Database limits</span></span>
<span data-ttu-id="b120d-255">Ограничения базы данных SQL описаны в разделе [Ограничения ресурсов базы данных SQL](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b120d-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b120d-256">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="b120d-256">See also</span></span>
[<span data-ttu-id="b120d-257">Основные сведения о лимитах Azure и их увеличении</span><span class="sxs-lookup"><span data-stu-id="b120d-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="b120d-258">Размеры виртуальных машин и облачных служб для Azure</span><span class="sxs-lookup"><span data-stu-id="b120d-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="b120d-259">Размеры для облачных служб</span><span class="sxs-lookup"><span data-stu-id="b120d-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

