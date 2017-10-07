---
title: "хранилище в памяти XTP aaaMonitor | Документы Microsoft"
description: "Сведения об оценке и мониторинге использования и емкости хранилища XTP в памяти и об устранении нехватки памяти 41823."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="25324-103">Мониторинг хранилища OLTP в памяти</span><span class="sxs-lookup"><span data-stu-id="25324-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="25324-104">При использовании [выполняющейся в памяти OLTP](sql-database-in-memory.md) данные в оптимизированных для памяти таблицах и переменные таблиц находятся в выполняющемся в памяти хранилище OLTP.</span><span class="sxs-lookup"><span data-stu-id="25324-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="25324-105">Каждая служба Premium имеет максимальный размер хранилища In-Memory OLTP, который описан в hello [статье уровни служб базы данных SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="25324-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="25324-106">При превышении этого ограничения операции вставки и обновления могут завершаться сбоем (ошибка 41823).</span><span class="sxs-lookup"><span data-stu-id="25324-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="25324-107">На этом этапе будет требуется tooeither удаления данных tooreclaim памяти или обновите hello уровня производительности базы данных.</span><span class="sxs-lookup"><span data-stu-id="25324-107">At that point you will need tooeither delete data tooreclaim memory, or upgrade hello performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a><span data-ttu-id="25324-108">Определить, будут ли данные не умещаются в cap hello хранилище в памяти</span><span class="sxs-lookup"><span data-stu-id="25324-108">Determine whether data will fit within hello in-memory storage cap</span></span>
<span data-ttu-id="25324-109">Определить ограничение хранилища hello: обратитесь к hello [статье уровни служб базы данных SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) для hello хранилища caps hello разных уровней служб Premium.</span><span class="sxs-lookup"><span data-stu-id="25324-109">Determine hello storage cap: consult hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for hello storage caps of hello different Premium service tiers.</span></span>

<span data-ttu-id="25324-110">Оценка памяти, что требования для оптимизированной для памяти таблицы работает hello таким же образом для SQL Server, как он выполняет в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="25324-110">Estimating memory requirements for a memory-optimized table works hello same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="25324-111">Отключите эту статью tooreview несколько минут на [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="25324-111">Take a few minutes tooreview that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="25324-112">Обратите внимание, что таблица hello и переменных строк таблицы, а также индексов, учитываются при определении размера данных hello max пользователя.</span><span class="sxs-lookup"><span data-stu-id="25324-112">Note that hello table and table variable rows, as well as indexes, count toward hello max user data size.</span></span> <span data-ttu-id="25324-113">Кроме того инструкции ALTER TABLE необходимо достаточное количество места toocreate новую версию hello всей таблицы и ее индексов.</span><span class="sxs-lookup"><span data-stu-id="25324-113">In addition, ALTER TABLE needs enough room toocreate a new version of hello entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="25324-114">Мониторинг и оповещения</span><span class="sxs-lookup"><span data-stu-id="25324-114">Monitoring and alerting</span></span>
<span data-ttu-id="25324-115">Вы можете отслеживать использование хранилища в памяти в процентах от hello [крепления хранилища для уровня производительности](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) в hello Azure [портала](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="25324-115">You can monitor in-memory storage use as a percentage of hello [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="25324-116">В колонке базы данных hello найдите поле использования ресурсов hello и щелкните изменить.</span><span class="sxs-lookup"><span data-stu-id="25324-116">On hello Database blade, locate hello Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="25324-117">Выберите метрику hello `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="25324-117">Then select hello metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="25324-118">tooadd оповещение, щелкните hello использование ресурсов поле tooopen hello колонка метрики, затем выберите команду добавить оповещение.</span><span class="sxs-lookup"><span data-stu-id="25324-118">tooadd an alert, click on hello Resource Utilization box tooopen hello Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="25324-119">Или используйте hello следующий запрос использование хранилища в памяти tooshow hello:</span><span class="sxs-lookup"><span data-stu-id="25324-119">Or use hello following query tooshow hello in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="25324-120">Исправление ситуаций с нехваткой памяти (ошибка 41823)</span><span class="sxs-lookup"><span data-stu-id="25324-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="25324-121">Нехватка памяти приводит к тому, что операции вставки, обновления и создания завершаются сбоем с сообщением об ошибке 41823.</span><span class="sxs-lookup"><span data-stu-id="25324-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="25324-122">Сообщение об ошибке 41823 означает, что hello оптимизированных для памяти таблицы и табличные переменные превысили максимальный размер hello.</span><span class="sxs-lookup"><span data-stu-id="25324-122">Error message 41823 indicates that hello memory-optimized tables and table variables have exceeded hello maximum size.</span></span>

<span data-ttu-id="25324-123">tooresolve эту ошибку, либо:</span><span class="sxs-lookup"><span data-stu-id="25324-123">tooresolve this error, either:</span></span>

* <span data-ttu-id="25324-124">Удалить данные из оптимизированных для памяти таблиц hello, потенциально разгрузки tootraditional данных hello, дисковых таблиц; или,</span><span class="sxs-lookup"><span data-stu-id="25324-124">Delete data from hello memory-optimized tables, potentially offloading hello data tootraditional, disk-based tables; or,</span></span>
* <span data-ttu-id="25324-125">Обновление tooone уровня службы hello недостаточно места в памяти для данных hello необходимо tookeep в таблицах, оптимизированных для памяти.</span><span class="sxs-lookup"><span data-stu-id="25324-125">Upgrade hello service tier tooone with enough in-memory storage for hello data you need tookeep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25324-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25324-126">Next steps</span></span>
<span data-ttu-id="25324-127">Инструкции по мониторингу см. в разделе [Мониторинг базы данных SQL Azure с помощью динамических представлений управления](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="25324-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
