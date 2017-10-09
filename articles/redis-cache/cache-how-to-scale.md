---
title: "aaaHow tooScale кэша Redis для Azure | Документы Microsoft"
description: "Узнайте, как tooscale Azure Redis кэш экземпляров"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a><span data-ttu-id="d1fc1-103">Как tooScale Redis для Azure кэша</span><span class="sxs-lookup"><span data-stu-id="d1fc1-103">How tooScale Azure Redis Cache</span></span>
<span data-ttu-id="d1fc1-104">Кэш Azure Redis имеет разные предложения кэша, которые обеспечивают гибкость при hello Выбор размера кэша и компоненты.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-104">Azure Redis Cache has different cache offerings, which provide flexibility in hello choice of cache size and features.</span></span> <span data-ttu-id="d1fc1-105">После создания кэша можно масштабировать размер hello и hello в ценовой категории hello кэша при изменении требований hello приложения.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-105">After a cache is created, you can scale hello size and hello pricing tier of hello cache if hello requirements of your application change.</span></span> <span data-ttu-id="d1fc1-106">В этой статье показано, как tooscale кэша как hello портал Azure, так и с помощью средств, таких как Azure PowerShell и Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-106">This article shows you how tooscale your cache in both hello Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-tooscale"></a><span data-ttu-id="d1fc1-107">Когда tooscale</span><span class="sxs-lookup"><span data-stu-id="d1fc1-107">When tooscale</span></span>
<span data-ttu-id="d1fc1-108">Можно использовать hello [мониторинг](cache-how-to-monitor.md) функции кэша Azure Redis toomonitor hello работоспособность и производительность кэша и определить, когда tooscale hello кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-108">You can use hello [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache toomonitor hello health and performance of your cache and help determine when tooscale hello cache.</span></span> 

<span data-ttu-id="d1fc1-109">Вы можете отслеживать следующие hello toohelp метрик выяснения того, требуются tooscale.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-109">You can monitor hello following metrics toohelp determine if you need tooscale.</span></span>

* <span data-ttu-id="d1fc1-110">Загрузка сервера Redis</span><span class="sxs-lookup"><span data-stu-id="d1fc1-110">Redis Server Load</span></span>
* <span data-ttu-id="d1fc1-111">Использование памяти</span><span class="sxs-lookup"><span data-stu-id="d1fc1-111">Memory Usage</span></span>
* <span data-ttu-id="d1fc1-112">Пропускная способность сети</span><span class="sxs-lookup"><span data-stu-id="d1fc1-112">Network Bandwidth</span></span>
* <span data-ttu-id="d1fc1-113">Загрузка ЦП</span><span class="sxs-lookup"><span data-stu-id="d1fc1-113">CPU Usage</span></span>

<span data-ttu-id="d1fc1-114">Если выяснилось, что ваш кэш больше не удовлетворяет требованиям приложения, можно масштабировать tooa увеличить или уменьшить размер кэша, ценовой категории, которая подходит для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-114">If you determine that your cache is no longer meeting your application's requirements, you can scale tooa larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="d1fc1-115">Дополнительные сведения об определении кэширования ценовой уровень toouse см. в разделе [какие Redis размер кэша и использовать](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="d1fc1-115">For more information on determining which cache pricing tier toouse, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="d1fc1-116">Масштабирование кэша</span><span class="sxs-lookup"><span data-stu-id="d1fc1-116">Scale a cache</span></span>
<span data-ttu-id="d1fc1-117">tooscale кэша, [Обзор кэша toohello](cache-configure.md#configure-redis-cache-settings) в hello [портал Azure](https://portal.azure.com) и нажмите кнопку **шкалы** из hello **ресурсов меню**.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-117">tooscale your cache, [browse toohello cache](cache-configure.md#configure-redis-cache-settings) in hello [Azure portal](https://portal.azure.com) and click **Scale** from hello **Resource menu**.</span></span>

![Масштаб](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="d1fc1-119">Выберите hello требуемого категория hello **выберите ценовую категорию** колонку и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-119">Select hello desired pricing tier from hello **Select pricing tier** blade and click **Select**.</span></span>

![Ценовая категория ][redis-cache-pricing-tier-blade]


<span data-ttu-id="d1fc1-121">Можно масштабировать tooa различных ценовой категории с hello следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="d1fc1-121">You can scale tooa different pricing tier with hello following restrictions:</span></span>

* <span data-ttu-id="d1fc1-122">Нельзя масштабировать из выше ценовой уровень tooa ниже ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-122">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="d1fc1-123">Нельзя масштабировать из **Premium** кэша вниз tooa **Стандартная** или **основные** кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-123">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="d1fc1-124">Нельзя масштабировать из **Стандартная** кэша вниз tooa **основные** кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-124">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="d1fc1-125">Можно масштабировать от **основные** кэшировать tooa **Стандартная** кэш, но не может изменить размер hello в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-125">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="d1fc1-126">Если требуется другой размер, можно сделать последующих размер toohello требуемой операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-126">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="d1fc1-127">Нельзя масштабировать из **основные** кэшировать непосредственно tooa **Premium** кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-127">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="d1fc1-128">Требуется расширение из **основные** слишком**Стандартная** за одну операцию масштабирования, а затем с **Стандартная** слишком**Premium** последующих масштабирования операция.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-128">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="d1fc1-129">Нельзя масштабировать от большего вниз toohello **C0 (250 МБ)** размер.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-129">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="d1fc1-130">Хотя hello кэша выполняется масштабирование toohello новые ценовой категории, **масштабирование** состояние отображается в hello **кэша Redis** колонку.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-130">While hello cache is scaling toohello new pricing tier, a **Scaling** status is displayed in hello **Redis Cache** blade.</span></span>

![Масштабирование][redis-cache-scaling]

<span data-ttu-id="d1fc1-132">По завершении масштабирование hello состояние меняется с **масштабирование** слишком**под управлением**.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-132">When scaling is complete, hello status changes from **Scaling** too**Running**.</span></span>

## <a name="how-tooautomate-a-scaling-operation"></a><span data-ttu-id="d1fc1-133">Как tooautomate операцию масштабирования</span><span class="sxs-lookup"><span data-stu-id="d1fc1-133">How tooautomate a scaling operation</span></span>
<span data-ttu-id="d1fc1-134">В дополнение tooscaling экземпляров кэша в Здравствуйте портал Azure, можно масштабировать, используя командлеты PowerShell Azure CLI и с помощью hello библиотеки управления Microsoft Azure (MAML).</span><span class="sxs-lookup"><span data-stu-id="d1fc1-134">In addition tooscaling your cache instances in hello Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using hello Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="d1fc1-135">Масштабирование с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1fc1-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="d1fc1-136">Масштабирование с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="d1fc1-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="d1fc1-137">Масштабирование с помощью MAML</span><span class="sxs-lookup"><span data-stu-id="d1fc1-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="d1fc1-138">Масштабирование с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1fc1-138">Scale using PowerShell</span></span>
<span data-ttu-id="d1fc1-139">Можно масштабировать экземпляров кэша Redis Azure с помощью PowerShell с помощью hello [набор AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) в случае, если hello `Size`, `Sku`, или `ShardCount` свойства изменяются.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-139">You can scale your Azure Redis Cache instances with PowerShell by using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="d1fc1-140">Hello следующем примере показано, как tooscale кэш именоваться `myCache` tooa 2,5 ГБ кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-140">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="d1fc1-141">Дополнительные сведения о масштабировании с помощью PowerShell см. в разделе [tooscale Redis кэша с помощью Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span><span class="sxs-lookup"><span data-stu-id="d1fc1-141">For more information on scaling with PowerShell, see [tooscale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="d1fc1-142">Масштабирование с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="d1fc1-142">Scale using Azure CLI</span></span>
<span data-ttu-id="d1fc1-143">вызывается с помощью Azure CLI экземплярами кэша Azure Redis tooscale hello `azure rediscache set` команды и передать hello необходимости изменения конфигурации, которые включают новый размер, sku или размер кластера, в зависимости от hello требуемого операцию масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-143">tooscale your Azure Redis Cache instances using Azure CLI, call hello `azure rediscache set` command and pass in hello desired configuration changes that include a new size, sku, or cluster size, depending on hello desired scaling operation.</span></span>

<span data-ttu-id="d1fc1-144">Дополнительные сведения о масштабировании с помощью интерфейса командной строки Azure см. в разделе [Изменение параметров существующего кэша Redis](cache-manage-cli.md#scale).</span><span class="sxs-lookup"><span data-stu-id="d1fc1-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="d1fc1-145">Масштабирование с помощью MAML</span><span class="sxs-lookup"><span data-stu-id="d1fc1-145">Scale using MAML</span></span>
<span data-ttu-id="d1fc1-146">tooscale экземпляров кэша Redis Azure с помощью hello [библиотеки управления Microsoft Azure (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), вызов hello `IRedisOperations.CreateOrUpdate` метод и передайте его в новый размер hello hello `RedisProperties.SKU.Capacity`.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-146">tooscale your Azure Redis Cache instances using hello [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call hello `IRedisOperations.CreateOrUpdate` method and pass in hello new size for hello `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="d1fc1-147">Дополнительные сведения см. в разделе hello [управления кэша Redis с помощью MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) образца.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-147">For more information, see hello [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="d1fc1-148">Масштабирование: часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="d1fc1-148">Scaling FAQ</span></span>
<span data-ttu-id="d1fc1-149">Hello следующий список содержит toocommonly ответы, вопросы и ответы о масштабировании кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-149">hello following list contains answers toocommonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="d1fc1-150">Можно ли выполнять масштабирование кэша до уровня Премиум, с уровня Премиум до другого уровня или в пределах уровня Премиум?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="d1fc1-151">После масштабирования, нужно ли toochange ключи кэша имени или доступа?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-151">After scaling, do I have toochange my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="d1fc1-152">Как работает масштабирование?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="d1fc1-153">Сохранятся ли данные кэша при масштабировании?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="d1fc1-154">Что происходит с пользовательским параметром databases при масштабировании?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="d1fc1-155">Будет ли кэш доступен во время масштабирования?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="d1fc1-156">Какие операции не поддерживаются?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="d1fc1-157">Сколько времени занимает масштабирование?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="d1fc1-158">Как узнать, когда масштабирование завершено?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="d1fc1-159">Можно ли выполнять масштабирование кэша до уровня Премиум, с уровня Премиум до другого уровня или в пределах уровня Премиум?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="d1fc1-160">Нельзя масштабировать из **Premium** кэша вниз tooa **основные** или **Стандартная** ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-160">You can't scale from a **Premium** cache down tooa **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="d1fc1-161">Можно масштабировать от одного **Premium** цены tooanother уровня кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-161">You can scale from one **Premium** cache pricing tier tooanother.</span></span>
* <span data-ttu-id="d1fc1-162">Нельзя масштабировать из **основные** кэшировать непосредственно tooa **Premium** кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-162">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="d1fc1-163">Сначала необходимо масштабирование из **основные** слишком**стандартные** за одну операцию масштабирования, а затем от **стандартные** слишком**Premium** в последующем Операция масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-163">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="d1fc1-164">Если включена кластеризация при создании вашего **Premium** кэша, вы можете [изменить размер кластера hello](cache-how-to-premium-clustering.md#cluster-size).</span><span class="sxs-lookup"><span data-stu-id="d1fc1-164">If you enabled clustering when you created your **Premium** cache, you can [change hello cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="d1fc1-165">Если кэш был создан без включенной кластеризации, ее нельзя будет настроить позже.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="d1fc1-166">Дополнительные сведения см. в разделе [как tooconfigure кластеризации для кэша Redis Azure Premium](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="d1fc1-166">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a><span data-ttu-id="d1fc1-167">После масштабирования, нужно ли toochange ключи кэша имени или доступа?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-167">After scaling, do I have toochange my cache name or access keys?</span></span>
<span data-ttu-id="d1fc1-168">Нет, имя кэша и ключи не изменяются во время операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="d1fc1-169">Как работает масштабирование?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-169">How does scaling work?</span></span>
* <span data-ttu-id="d1fc1-170">Когда **основные** кэш масштабируется tooa другого размера, она завершает работу, а новый кэш, предоставляется с помощью нового размера hello.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-170">When a **Basic** cache is scaled tooa different size, it is shut down and a new cache is provisioned using hello new size.</span></span> <span data-ttu-id="d1fc1-171">В течение этого времени hello кэша недоступна и все данные в кэше hello, будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-171">During this time, hello cache is unavailable and all data in hello cache is lost.</span></span>
* <span data-ttu-id="d1fc1-172">При **основные** кэш является масштабированный tooa **Стандартная** кэш, Подготовка кэша-реплики и hello данные копируются из hello основной toohello реплики кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-172">When a **Basic** cache is scaled tooa **Standard** cache, a replica cache is provisioned and hello data is copied from hello primary cache toohello replica cache.</span></span> <span data-ttu-id="d1fc1-173">во время процесса масштабирование hello Hello кэш остается доступным.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-173">hello cache remains available during hello scaling process.</span></span>
* <span data-ttu-id="d1fc1-174">При **Стандартная** кэш является другой длины масштабированные tooa или tooa **Premium** кэша, одна из реплик hello завершает работу и повторно подготовить toohello новый размер и hello передача данных по и других hello реплика выполнит переход на другой ресурс перед его повторно инициализировать, аналогичный процесс toohello, возникающее при сбое одного из узлов кэша hello.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-174">When a **Standard** cache is scaled tooa different size or tooa **Premium** cache, one of hello replicas is shut down and re-provisioned toohello new size and hello data transferred over, and then hello other replica performs a failover before it is re-provisioned, similar toohello process that occurs during a failure of one of hello cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="d1fc1-175">Сохранятся ли данные кэша при масштабировании?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="d1fc1-176">Когда **основные** кэша находится новый размер масштабированный tooa, все данные теряются и hello кэша недоступна во время операция масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-176">When a **Basic** cache is scaled tooa new size, all data is lost and hello cache is unavailable during hello scaling operation.</span></span>
* <span data-ttu-id="d1fc1-177">При **основные** кэш является масштабированный tooa **Стандартная** кэша, hello кэша hello обычно сохраняются данные.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-177">When a **Basic** cache is scaled tooa **Standard** cache, hello data in hello cache is typically preserved.</span></span>
* <span data-ttu-id="d1fc1-178">При **Стандартная** кэш является масштабированный tooa большего размера или уровень, или **Premium** кэш масштабируется tooa больший размер, все данные, обычно сохраняются.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-178">When a **Standard** cache is scaled tooa larger size or tier, or a **Premium** cache is scaled tooa larger size, all data is typically preserved.</span></span> <span data-ttu-id="d1fc1-179">При масштабировании **Стандартная** или **Premium** кэша вниз tooa меньшего размера, данные могут быть потеряны в зависимости от того, сколько данных находится в кэше hello связанных новый размер toohello при масштабировании.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-179">When scaling a **Standard** or **Premium** cache down tooa smaller size, data may be lost depending on how much data is in hello cache related toohello new size when it is scaled.</span></span> <span data-ttu-id="d1fc1-180">При потере данных при масштабировании с уменьшением, ключи извлекаются с помощью hello [allkeys lru](http://redis.io/topics/lru-cache) политики вытеснения.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-180">If data is lost when scaling down, keys are evicted using hello [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="d1fc1-181">Что происходит с пользовательским параметром databases при масштабировании?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="d1fc1-182">Некоторые ценовые категории имеют различные [баз данных ограничения](cache-configure.md#databases), поэтому существуют определенные рекомендации, если масштабирование Если настроено пользовательское значение hello `databases` можно задать во время создания кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="d1fc1-183">При масштабировании tooa ценовой категории с более низким `databases` предел от текущего уровня hello:</span><span class="sxs-lookup"><span data-stu-id="d1fc1-183">When scaling tooa pricing tier with a lower `databases` limit than hello current tier:</span></span>
  * <span data-ttu-id="d1fc1-184">Если вы используете hello количество по умолчанию `databases` которого составляет 16 для всех ценовых категорий, данные не потеряны.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-184">If you are using hello default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="d1fc1-185">Если вы используете настраиваемое число `databases` , находящееся в пределах hello toowhich уровня hello, будет произведено масштабирование, это `databases` настройки сохраняются, и данные не теряются.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-185">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="d1fc1-186">При использовании настраиваемое число `databases` , размер которого превышает ограничения hello hello новый уровень, hello `databases` параметр задается для ограничений снижения toohello на новый уровень hello и потере всех данных в базах данных удалены hello.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-186">If you are using a custom number of `databases` that exceeds hello limits of hello new tier, hello `databases` setting is lowered toohello limits of hello new tier and all data in hello removed databases is lost.</span></span>
* <span data-ttu-id="d1fc1-187">При масштабировании же или более поздней версии в ценовой категории с hello tooa `databases` предел от текущего уровня hello вашей `databases` настройки сохраняются, и данные не теряются.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-187">When scaling tooa pricing tier with hello same or higher `databases` limit than hello current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="d1fc1-188">Обратите внимание, что, хотя кэш "Стандартный" и "Премиум" имеет соглашение об уровне обслуживания с показателем доступности 99,9 %, для потери данных соглашение об уровне обслуживания отсутствует.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="d1fc1-189">Будет ли кэш доступен во время масштабирования?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="d1fc1-190">**Стандартная** и **Premium** кэши остаются доступными во время операция масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-190">**Standard** and **Premium** caches remain available during hello scaling operation.</span></span>
* <span data-ttu-id="d1fc1-191">**Основные** кэши находятся в автономном режиме во время масштабирования операций tooa разного размера, но остаются доступными при масштабировании с **основные** слишком**Standard**.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-191">**Basic** caches are offline during scaling operations tooa different size, but remain available when scaling from **Basic** too**Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="d1fc1-192">Какие операции не поддерживаются?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-192">Operations that are not supported</span></span>
* <span data-ttu-id="d1fc1-193">Нельзя масштабировать из выше ценовой уровень tooa ниже ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-193">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="d1fc1-194">Нельзя масштабировать из **Premium** кэша вниз tooa **Стандартная** или **основные** кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-194">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="d1fc1-195">Нельзя масштабировать из **Стандартная** кэша вниз tooa **основные** кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-195">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="d1fc1-196">Можно масштабировать от **основные** кэшировать tooa **Стандартная** кэш, но не может изменить размер hello в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-196">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="d1fc1-197">Если требуется другой размер, можно сделать последующих размер toohello требуемой операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-197">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="d1fc1-198">Нельзя масштабировать из **основные** кэшировать непосредственно tooa **Premium** кэша.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-198">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="d1fc1-199">Сначала необходимо масштабирование из **основные** слишком**стандартные** за одну операцию масштабирования, а затем от **стандартные** слишком**Premium** в последующем Операция масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-199">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="d1fc1-200">Нельзя масштабировать от большего вниз toohello **C0 (250 МБ)** размер.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-200">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>

<span data-ttu-id="d1fc1-201">Если происходит сбой операции масштабирования, hello служба попытается toorevert hello операции и кэша hello вернется toohello исходный размер.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-201">If a scaling operation fails, hello service will try toorevert hello operation and hello cache will revert toohello original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="d1fc1-202">Сколько времени занимает масштабирование?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-202">How long does scaling take?</span></span>
<span data-ttu-id="d1fc1-203">Масштабирование занимает приблизительно 20 минут, в зависимости от того, сколько данных находится в кэше hello.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-203">Scaling takes approximately 20 minutes, depending on how much data is in hello cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="d1fc1-204">Как узнать, когда масштабирование завершено?</span><span class="sxs-lookup"><span data-stu-id="d1fc1-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="d1fc1-205">Hello портала Azure вы увидите hello операцию масштабирования в данный момент.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-205">In hello Azure portal you can see hello scaling operation in progress.</span></span> <span data-ttu-id="d1fc1-206">По завершении масштабирование hello hello состояния кэша слишком**под управлением**.</span><span class="sxs-lookup"><span data-stu-id="d1fc1-206">When scaling is complete, hello status of hello cache changes too**Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



