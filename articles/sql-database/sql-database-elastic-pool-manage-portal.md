---
title: "Портал Azure: создание пула эластичных баз данных SQL и управление им | Документация Майкрософт"
description: "Узнайте, как toouse hello портал Azure и toomanage интеллектуальным базы данных SQL, монитор и верного размера производительность базы данных toooptimize масштабируемой эластичного пула и управлять затрат."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="c0e2a-103">Создание и управление ими в пуле эластичных БД с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c0e2a-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="c0e2a-104">В этом разделе показано, как toocreate и управления ими масштабируемой [эластичные пулы](sql-database-elastic-pool.md) с hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="c0e2a-105">Можно также создать и управлять Azure эластичного пула с [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API или [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="c0e2a-106">Вы также можете использовать [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), чтобы создавать новые базы данных в эластичных пулах и перемещать базы данных в пулы и обратно.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="c0e2a-107">Создание эластичного пула</span><span class="sxs-lookup"><span data-stu-id="c0e2a-107">Create an elastic pool</span></span> 

<span data-ttu-id="c0e2a-108">Эластичный пул можно создать двумя способами.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="c0e2a-109">Если вы знаете hello пула установки требуется, или начинаться с рекомендацией из службы hello можно сделать ее с нуля.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="c0e2a-110">База данных SQL имеет интеллектуальным рекомендует при установке эластичного пула, если это более экономичное решение в зависимости от hello предыдущие данные телеметрии использования для баз данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="c0e2a-111">Можно создать несколько пулов на сервере, но нельзя добавить баз данных с разных серверов в hello одного пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="c0e2a-112">Пулы эластичных БД общедоступны во всех регионах Azure, кроме западной Индии, где сейчас доступна только предварительная версия.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="c0e2a-113">Общедоступные пулы эластичных БД появятся в этом регионе в самое ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="c0e2a-114">Шаг 1. Создание эластичного пула</span><span class="sxs-lookup"><span data-stu-id="c0e2a-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="c0e2a-115">Создание из существующего эластичного пула **сервера** панель hello портала — это hello простым способом toomove существующих баз данных в эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="c0e2a-116">Можно также создать эластичного пула, выполняя поиск **гибкий пул SQL** в hello **Marketplace** или щелкнув **+ добавить** в hello **пулах эластичных БД SQL**Обзор колонку.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="c0e2a-117">Все возможности toospecify на новый или существующий сервер через этот пул, рабочий процесс подготовки.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="c0e2a-118">В hello [портал Azure](http://portal.azure.com/), нажмите кнопку **дополнительные службы**  **>**  **серверов SQL Server**и нажмите кнопку hello сервер, содержащий hello Вы хотите tooadd tooan эластичного пула баз данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="c0e2a-119">Щелкните **Создать пул**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-119">Click **New pool**.</span></span>

    ![Добавление пула tooa сервера](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="c0e2a-121">**-ИЛИ-**</span><span class="sxs-lookup"><span data-stu-id="c0e2a-121">**-OR-**</span></span>

    <span data-ttu-id="c0e2a-122">Может появиться сообщение о том, что рекомендуется использовать эластичные пулы для сервера hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="c0e2a-123">Щелкните hello toosee сообщение hello, рекомендуемые пулы основании данные телеметрии использования журнала базы данных, выберите toosee уровня hello Дополнительные сведения и настройки пула hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="c0e2a-124">В разделе [понять пула рекомендаций](#understand-elastic-pool-recommendations) далее в этом разделе как hello рекомендации.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![рекомендуемый пул](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="c0e2a-126">Hello **эластичного пула** колонке отображается которого задается hello параметры для пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="c0e2a-127">Если вы нажали кнопку **новый пул** hello в предыдущем шаге, является hello ценовой категории **стандартные** по умолчанию и базы данных не выбран.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="c0e2a-128">Можно создать пул пустой или выбрать несколько баз данных из этого toomove сервера в пул hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="c0e2a-129">При создании рекомендуемый пул hello рекомендуется ценовой категории параметров производительности и подставляются список баз данных, но может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Настройка эластичного пула](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="c0e2a-131">Укажите имя для эластичного пула hello, или оставьте его значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="c0e2a-132">Шаг 2. Выбор ценовой категории</span><span class="sxs-lookup"><span data-stu-id="c0e2a-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="c0e2a-133">Hello пула Ценовая категория определяет hello преимущества доступных toohello elastics в пул hello и hello максимальное число edtu, которое (eDTU MAX) и базы данных доступны tooeach хранилища (ГБ).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="c0e2a-134">Дополнительные сведения см. в статье "Уровни служб".</span><span class="sxs-lookup"><span data-stu-id="c0e2a-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="c0e2a-135">Щелкните toochange hello ценовую категорию для пула hello **Ценовая категория**, нажмите кнопку hello ценовой категории и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0e2a-136">После Выбор ценовой категории hello и фиксация изменений, нажав кнопку **ОК** на последнем шаге hello не будет возможности toochange hello ценовой категории hello пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="c0e2a-137">toochange hello ценовую категорию существующего пула эластичных БД, создать эластичного пула в нужный ценовой категории hello перенести hello баз данных toothis новый пул.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![Выберите ценовую категорию](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="c0e2a-139">Шаг 3: Настройка пула hello</span><span class="sxs-lookup"><span data-stu-id="c0e2a-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="c0e2a-140">После настройки hello ценовой категории, нажмите кнопку Настройка пула, добавления базы данных, набор Edtu пула и хранилища (пул ГБ), а значение hello min и max число Edtu для hello elastics в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="c0e2a-141">Щелкните **Настроить пул**</span><span class="sxs-lookup"><span data-stu-id="c0e2a-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="c0e2a-142">Выберите базы данных hello требуется tooadd toohello пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="c0e2a-143">Этот шаг необязателен при создании пула hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="c0e2a-144">Базы данных можно добавить после создания пула hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="c0e2a-145">tooadd баз данных, нажмите кнопку **добавления базы данных**, щелкните hello баз данных требуется tooadd и нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![Добавить базы данных](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="c0e2a-147">Здравствуйте, если вы работаете с базами данных hello достаточно данных телеметрии истории использования, **Оценка использования eDTU и ГБ** диаграммы и hello **фактический объем использования eDTU** toohelp обновление линейчатая диаграмма, конфигурации решения.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="c0e2a-148">Кроме того, служба hello может привести к toohelp сообщение рекомендации вы верного размера hello пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="c0e2a-149">В разделе [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="c0e2a-150">Использование элементов управления hello в hello **настроить пул** tooexplore параметров страницы и настроить пул.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="c0e2a-151">Дополнительные сведения об ограничениях для каждого уровня обслуживания см. в разделе [eDTU и размеры хранилища для пулов эластичных БД](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools). Подробные рекомендации по выбору правильного размера эластичного пула см. в статье [Когда следует использовать эластичный пул?](sql-database-elastic-pool.md)</span><span class="sxs-lookup"><span data-stu-id="c0e2a-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="c0e2a-152">Дополнительные сведения о параметрах пула см. в разделе [Свойства пулов эластичных БД](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Настройка эластичного пула](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="c0e2a-154">Нажмите кнопку **выберите** в hello **настроить пул** колонке после изменения параметров.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="c0e2a-155">Нажмите кнопку **ОК** toocreate hello пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="c0e2a-156">Пояснения к рекомендациям для эластичного пула</span><span class="sxs-lookup"><span data-stu-id="c0e2a-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="c0e2a-157">Hello служба базы данных SQL оценивает журнал использования и рекомендует один или несколько пулов, когда это эффективнее, чем при использовании одной базы данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="c0e2a-158">Каждая рекомендация оснащен уникальное подмножество hello сервера баз данных, которые лучше всего соответствуют hello пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![рекомендуемый пул](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="c0e2a-160">Рекомендация Hello пул состоит из:</span><span class="sxs-lookup"><span data-stu-id="c0e2a-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="c0e2a-161">Ценовая категория для пула hello (Basic, Standard, Premium или Premium RS)</span><span class="sxs-lookup"><span data-stu-id="c0e2a-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="c0e2a-162">соответствующее количество **единиц eDTU пула** (также называемое максимальным количеством единиц eDTU для одного пула);</span><span class="sxs-lookup"><span data-stu-id="c0e2a-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="c0e2a-163">Hello **eDTU MAX** и **eDTU Min** каждой базы данных</span><span class="sxs-lookup"><span data-stu-id="c0e2a-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="c0e2a-164">Hello список рекомендуемых баз данных для пула hello</span><span class="sxs-lookup"><span data-stu-id="c0e2a-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0e2a-165">Служба Hello учитывает hello последние 30 дней телеметрии при рекомендации пулов.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="c0e2a-166">Для toobe базы данных, считаются кандидатом для эластичного пула он должен существовать по крайней мере в течение 7 дней.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="c0e2a-167">Базы данных, которые уже находятся в эластичном пуле, не рассматриваются в качестве кандидатов для рекомендуемого добавления в пул.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="c0e2a-168">Служба Hello оценивает потребностей в ресурсах и экономическую эффективность скользящего hello одной базы данных на каждом уровне службы в пулы hello же уровня.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="c0e2a-169">Например, все базы данных Standard на сервере оцениваются на предмет возможности их добавления в пул эластичных баз данных уровня Standard.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="c0e2a-170">Это означает, что служба hello не предоставить рекомендации между уровнями например стандартной базы данных в пул Premium.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="c0e2a-171">После добавления базы данных toohello пула, динамически создаются рекомендации на основе истории использования hello hello баз данных, которые вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="c0e2a-172">Эти рекомендации отображаются только в hello eDTU и ГБ диаграмма использования и рекомендации заголовка вверху hello hello **настроить пул** колонку.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="c0e2a-173">Эти рекомендации относятся предполагаемого tooassist вам в создании эластичного пула оптимизированными для конкретных баз данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![Динамические рекомендации](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="c0e2a-175">Мониторинг эластичного пула и управление им</span><span class="sxs-lookup"><span data-stu-id="c0e2a-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="c0e2a-176">Можно использовать hello Azure toomonitor портала и управления эластичного пула и базами данных hello в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="c0e2a-177">Из портала hello можно наблюдать за hello эластичного пула и баз данных hello этого пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="c0e2a-178">Можно также сделать эластичного пула tooyour набор изменений и отправить все изменения в hello, же время.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="c0e2a-179">К таким изменениям относятся добавление или удаление баз данных, изменение параметров эластичного пула и изменение параметров базы данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="c0e2a-180">Hello следующий рисунок показывает пример эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="c0e2a-181">Hello включает в себя:</span><span class="sxs-lookup"><span data-stu-id="c0e2a-181">hello view includes:</span></span>

*  <span data-ttu-id="c0e2a-182">Диаграммы для наблюдения за использованием ресурсов для эластичного пула hello и hello баз данных, содержащихся в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="c0e2a-183">Hello **Настройка** toomake кнопку пула изменяет toohello эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="c0e2a-184">Hello **создать базу данных** кнопки, которая создает базу данных и добавляет его toohello текущего пула эластичных БД.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="c0e2a-185">Задания обработки эластичных БД, которые помогают управлять большим количеством баз данных, запуская скрипты Transact-SQL для всех баз данных в списке.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Представление пула][2]

<span data-ttu-id="c0e2a-187">Вы можете перейти toosee tooa конкретного пула его использования ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="c0e2a-188">По умолчанию hello пула является настроенным tooshow использования хранилища и eDTU для hello последний час.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="c0e2a-189">Hello диаграмма может быть настроенный tooshow различных показателей по различным временным окнам.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="c0e2a-190">Выберите toowork пула эластичных БД с.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="c0e2a-191">В разделе **Наблюдение за пулами эластичных БД** есть диаграмма **Использование ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="c0e2a-192">Щелкните диаграмму hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-192">Click hello chart.</span></span>

    ![Мониторинг эластичного пула][3]

    <span data-ttu-id="c0e2a-194">Hello **метрика** открывает колонку, показывающая подробное представление hello заданных метрики hello указанного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![Выноска "Метрика"][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="c0e2a-196">Отображение диаграмм toocustomize hello</span><span class="sxs-lookup"><span data-stu-id="c0e2a-196">toocustomize hello chart display</span></span>

<span data-ttu-id="c0e2a-197">Другие показатели, например процент ЦП, процент операций ввода-ВЫВОДА данных и процент операций ввода-ВЫВОДА журнала, используемый можно редактировать диаграммы hello и toodisplay колонка метрики hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="c0e2a-198">Щелкните hello колонка метрики, **изменить**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-198">On hello metric blade, click **Edit**.</span></span>

    ![Щелкните "Изменить".][6]

2. <span data-ttu-id="c0e2a-200">В hello **изменить диаграмму** колонке выберите диапазон времени (за последний час, в настоящее время или прошлая неделя), или нажмите кнопку **пользовательские** tooselect любую дату в диапазоне hello последние две недели.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="c0e2a-201">Выберите тип диаграммы hello (линия или), а затем toomonitor ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="c0e2a-202">Только диаграмма показателей с hello же единицу измерения могут быть отображены в hello в hello же время.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="c0e2a-203">Например если выбрать «eDTU в процентах» затем можно выбрать только других метрик процент как hello единицы измерения.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![Щелкните "Изменить".](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="c0e2a-205">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="c0e2a-206">Мониторинг баз данных в эластичном пуле и управление ими</span><span class="sxs-lookup"><span data-stu-id="c0e2a-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="c0e2a-207">Отдельные базы данных также можно отслеживать на наличие потенциальных проблем.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="c0e2a-208">В разделе **Мониторинг эластичных баз данных**есть диаграмма, на которой отображаются метрики для пяти баз данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="c0e2a-209">По умолчанию hello диаграмма отображает hello 5 баз данных в пуле hello по объем использования eDTU среднее в hello последний час.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="c0e2a-210">Щелкните диаграмму hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-210">Click hello chart.</span></span>

    ![Мониторинг эластичного пула][4]

2. <span data-ttu-id="c0e2a-212">Hello **использования ресурсов базы данных** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="c0e2a-213">Это предоставляет подробное представление об использовании hello базы данных в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="c0e2a-214">С помощью сетки hello в нижней части колонки hello hello, можно выбрать все базы данных в пуле toodisplay hello его использования в диаграмме hello (копирование баз данных too5).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="c0e2a-215">Можно также настроить hello метрики времени окна и отображается в диаграмме hello, щелкнув **изменение диаграммы**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![Колонка "Использование ресурсов баз данных"][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="c0e2a-217">представление toocustomize hello</span><span class="sxs-lookup"><span data-stu-id="c0e2a-217">toocustomize hello view</span></span>

1. <span data-ttu-id="c0e2a-218">В hello **базы данных об использовании ресурсов** колонка, щелкните **изменение диаграммы**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Элемент управления "Изменение диаграммы"](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="c0e2a-220">В hello **изменить** диаграммы колонке выберите диапазон времени (за последний час или за последние 24 часа) или щелкните **пользовательские** tooselect различных ежедневно, hello за toodisplay 2 недели.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![Элемент управления "Пользовательский"](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="c0e2a-222">Щелкните hello **баз данных путем сравнения** tooselect раскрывающийся список различные метрики toouse при сравнении баз данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![Изменение диаграммы hello](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="c0e2a-224">toomonitor tooselect баз данных</span><span class="sxs-lookup"><span data-stu-id="c0e2a-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="c0e2a-225">В списке баз данных hello в hello **использования ресурсов базы данных** колонки, можно найти конкретных баз данных путем поиска по страницам hello в списке hello или ввести в hello имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="c0e2a-226">Используйте hello флажок tooselect hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-226">Use hello checkbox tooselect hello database.</span></span>

![Поиск toomonitor баз данных][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="c0e2a-228">Добавление оповещений tooan эластичного пула ресурсов</span><span class="sxs-lookup"><span data-stu-id="c0e2a-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="c0e2a-229">Можно добавить правила tooan пула эластичных БД, отправки электронной почты предупреждения или toopeople tooURL строки конечных точек, достигнув порог загрузки, которую вы настроили hello эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="c0e2a-230">**tooadd ресурс предупреждения tooany:**</span><span class="sxs-lookup"><span data-stu-id="c0e2a-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="c0e2a-231">Щелкните hello **использование ресурсов** tooopen hello диаграммы **метрика** колонке нажмите кнопку **добавить оповещение**и затем заполнить сведения hello в hello **добавить оповещение правило** колонке (**ресурсов** выполняется автоматическая настройка пула toobe hello, которым вы работаете).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="c0e2a-232">Введите значение **имя** и **описание** , идентифицирующий предупреждения tooyou hello и получателей hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="c0e2a-233">Выберите **метрика** нужных tooalert из списка hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="c0e2a-234">Диаграмма Hello динамически показано использование ресурсов для этой метрики toohelp выберите пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="c0e2a-235">Выберите **Условие** (больше, меньше и т. д.) и **Пороговое значение**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="c0e2a-236">Выберите **период** hello метрику времени правила должны соблюдаться hello предупреждения триггеры.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="c0e2a-237">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-237">Click **OK**.</span></span>

<span data-ttu-id="c0e2a-238">Дополнительные сведения см. в статье [Создание оповещений для базы данных SQL Azure с помощью портала Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="c0e2a-239">Перемещение базы данных в пул эластичных БД</span><span class="sxs-lookup"><span data-stu-id="c0e2a-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="c0e2a-240">Вы можете добавить или удалить базы данных из существующего пула.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="c0e2a-241">Hello могут находиться в других пулов.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-241">hello databases can be in other pools.</span></span> <span data-ttu-id="c0e2a-242">Тем не менее, можно добавить только базы данных, которые находятся на hello же логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="c0e2a-243">В колонке hello для пула hello под **эластичных баз данных** щелкните **настроить пул**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Щелкните "Настроить пул".][1]

2. <span data-ttu-id="c0e2a-245">В hello **настроить пул** колонка, щелкните **добавить toopool**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![Нажмите кнопку Добавить toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="c0e2a-247">В hello **добавления баз данных** колонки, базы данных выберите hello или пула toohello tooadd баз данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="c0e2a-248">Затем щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-248">Then click **Select**.</span></span>

    ![Выберите tooadd баз данных](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="c0e2a-250">Hello **настроить пул** колонке теперь списки hello базы данных, выбранной toobe добавлена с его состоянием, задайте слишком**ожидающие**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![Добавление в пул в состоянии ожидания.](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="c0e2a-252">В hello **Настройка пула колонке**, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Щелкните Сохранить](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="c0e2a-254">Перемещение базы данных из пула эластичных БД</span><span class="sxs-lookup"><span data-stu-id="c0e2a-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="c0e2a-255">В hello **настроить пул** колонки, базы данных выберите hello или tooremove баз данных.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![список баз данных](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="c0e2a-257">Щелкните **Удалить из пула**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-257">Click **Remove from pool**.</span></span>

    ![список баз данных](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="c0e2a-259">Hello **настроить пул** колонке теперь списки hello базы данных, выбранной toobe удаляется вместе с его статус слишком**ожидающие**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![Просмотр результата добавления и удаления базы данных](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="c0e2a-261">В hello **Настройка пула колонке**, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Щелкните Сохранить](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="c0e2a-263">Изменение параметров производительности эластичного пула</span><span class="sxs-lookup"><span data-stu-id="c0e2a-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="c0e2a-264">При наблюдении за использование ресурсов hello эластичного пула, вы можете заметить, что некоторые изменения требуются.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="c0e2a-265">Может быть hello потребности в изменении hello ограничения производительности или хранения.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="c0e2a-266">Возможно параметры toochange hello базы данных в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="c0e2a-267">Можно изменить настройки hello пула hello в любое время tooget hello оптимальный баланс производительности и стоимости.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="c0e2a-268">Дополнительные сведения см. в статье [Когда следует использовать пул эластичных баз данных?](sql-database-elastic-pool.md)</span><span class="sxs-lookup"><span data-stu-id="c0e2a-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="c0e2a-269">toochange hello число Edtu или хранилище ограничения в расчете на пул и Edtu на базу данных:</span><span class="sxs-lookup"><span data-stu-id="c0e2a-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="c0e2a-270">Откройте hello **настроить пул** колонку.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="c0e2a-271">В разделе **параметры эластичного пула**, используйте либо параметры пула hello toochange ползунка.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![Использование ресурсов пула эластичных БД](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="c0e2a-273">При изменении приветствия, экрана приветствия показывает hello предполагаемые ежемесячные затраты на изменения hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![Обновление эластичного пула и новые ежемесячные затраты](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="c0e2a-275">Задержка операций эластичного пула</span><span class="sxs-lookup"><span data-stu-id="c0e2a-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="c0e2a-276">Изменение hello min edtu, которое каждой базы данных или максимальное число Edtu на базу данных обычно завершает более 5 минут.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="c0e2a-277">Изменение hello число Edtu на пул, зависит от hello общий объем пространства, используемого всех баз данных в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="c0e2a-278">Изменение занимает порядка 90 минут или меньше на каждые 100 ГБ.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="c0e2a-279">Например если hello общее пространство, занимаемое всех баз данных в пуле hello составляет 200 ГБ, то hello ожидаемого задержка для изменения hello eDTU пула на пул — 3 часа или менее.</span><span class="sxs-lookup"><span data-stu-id="c0e2a-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0e2a-280">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0e2a-280">Next steps</span></span>

- <span data-ttu-id="c0e2a-281">toounderstand какие эластичного пула в разделе [эластичный пул баз данных SQL](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="c0e2a-282">Рекомендации по использованию эластичных пулов см. в статье [Когда следует использовать эластичный пул?](sql-database-elastic-pool.md)</span><span class="sxs-lookup"><span data-stu-id="c0e2a-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="c0e2a-283">toouse эластичной задания toorun Transact-SQL скрипты на любом количестве баз данных в пуле hello. в разделе [Обзор эластичной задания](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="c0e2a-284">tooquery через любое количество баз данных в пуле hello. в разделе [Обзор эластичной запросов](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="c0e2a-285">Для транзакций любое количество баз данных в пуле hello. в разделе [эластичной транзакции](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0e2a-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
