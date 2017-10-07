---
title: "aaaMigrate toopremium хранилища в хранилище Azure существующих данных | Документы Microsoft"
description: "Инструкции по переносу существующих toopremium хранилища данных"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="55a3a-103">Перенос toopremium хранение данных</span><span class="sxs-lookup"><span data-stu-id="55a3a-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="55a3a-104">В хранилище данных SQL Azure недавно реализована возможность использовать [хранилище класса Premium, чтобы обеспечить более предсказуемую производительность][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="55a3a-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="55a3a-105">Существующие данные складов в настоящее время в стандартном хранилище теперь могут быть перенесены toopremium хранилища.</span><span class="sxs-lookup"><span data-stu-id="55a3a-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="55a3a-106">Можно воспользоваться преимуществами автоматическая миграция, или если вы предпочитаете toocontrol при toomigrate (которая включает в себя некоторое время простоя), можно сделать самостоятельно hello миграции.</span><span class="sxs-lookup"><span data-stu-id="55a3a-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="55a3a-107">Если имеется более одного хранилища данных, используйте hello [расписание автоматического переноса] [ automatic migration schedule] toodetermine, когда следует выполнять миграцию.</span><span class="sxs-lookup"><span data-stu-id="55a3a-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="55a3a-108">Определение типа хранилища</span><span class="sxs-lookup"><span data-stu-id="55a3a-108">Determine storage type</span></span>
<span data-ttu-id="55a3a-109">При создании хранилища данных перед hello после даты, используемой в текущий момент стандартное хранилище.</span><span class="sxs-lookup"><span data-stu-id="55a3a-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="55a3a-110">**Регион**</span><span class="sxs-lookup"><span data-stu-id="55a3a-110">**Region**</span></span> | <span data-ttu-id="55a3a-111">**Хранилище данных, созданное до указанной даты**</span><span class="sxs-lookup"><span data-stu-id="55a3a-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="55a3a-112">Восточная часть Австралии</span><span class="sxs-lookup"><span data-stu-id="55a3a-112">Australia East</span></span> |<span data-ttu-id="55a3a-113">Хранилище класса Premium пока недоступно</span><span class="sxs-lookup"><span data-stu-id="55a3a-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="55a3a-114">Восток Китая</span><span class="sxs-lookup"><span data-stu-id="55a3a-114">China East</span></span> |<span data-ttu-id="55a3a-115">1 ноября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-115">November 1, 2016</span></span> |
| <span data-ttu-id="55a3a-116">Север Китая</span><span class="sxs-lookup"><span data-stu-id="55a3a-116">China North</span></span> |<span data-ttu-id="55a3a-117">1 ноября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-117">November 1, 2016</span></span> |
| <span data-ttu-id="55a3a-118">Центральная Германия</span><span class="sxs-lookup"><span data-stu-id="55a3a-118">Germany Central</span></span> |<span data-ttu-id="55a3a-119">1 ноября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-119">November 1, 2016</span></span> |
| <span data-ttu-id="55a3a-120">Северо-восточная Германия</span><span class="sxs-lookup"><span data-stu-id="55a3a-120">Germany Northeast</span></span> |<span data-ttu-id="55a3a-121">1 ноября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-121">November 1, 2016</span></span> |
| <span data-ttu-id="55a3a-122">Западная Индия</span><span class="sxs-lookup"><span data-stu-id="55a3a-122">India West</span></span> |<span data-ttu-id="55a3a-123">Хранилище класса Premium пока недоступно</span><span class="sxs-lookup"><span data-stu-id="55a3a-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="55a3a-124">Западная часть Японии</span><span class="sxs-lookup"><span data-stu-id="55a3a-124">Japan West</span></span> |<span data-ttu-id="55a3a-125">Хранилище класса Premium пока недоступно</span><span class="sxs-lookup"><span data-stu-id="55a3a-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="55a3a-126">Северо-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="55a3a-126">North Central US</span></span> |<span data-ttu-id="55a3a-127">10 ноября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="55a3a-128">Сведения об автоматической миграции</span><span class="sxs-lookup"><span data-stu-id="55a3a-128">Automatic migration details</span></span>
<span data-ttu-id="55a3a-129">По умолчанию, мы перенесем базы данных автоматически между 6:00 и 6:00:00 по местному времени для своего региона во время hello [расписание автоматического переноса][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="55a3a-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="55a3a-130">Хранилище данных будет невозможно использовать во время миграции hello.</span><span class="sxs-lookup"><span data-stu-id="55a3a-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="55a3a-131">Hello миграции занимает примерно один час в расчете на терабайт хранилища в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="55a3a-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="55a3a-132">Вы не будете платить во время любой части hello автоматическую миграцию.</span><span class="sxs-lookup"><span data-stu-id="55a3a-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="55a3a-133">После завершения переноса hello, хранилищем данных будет снова документации и может использоваться.</span><span class="sxs-lookup"><span data-stu-id="55a3a-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="55a3a-134">Корпорация Майкрософт занимает hello следующие шаги toocomplete hello миграции (эти файлы не требуют любой вмешательства со стороны пользователя).</span><span class="sxs-lookup"><span data-stu-id="55a3a-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="55a3a-135">В этом примере мы рассмотрим существующее хранилище данных с именем MyDW, размещенное в хранилище класса Standard.</span><span class="sxs-lookup"><span data-stu-id="55a3a-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="55a3a-136">Microsoft переименовывает «MyDW» слишком «MyDW_DO_NOT_USE_ [Timestamp]».</span><span class="sxs-lookup"><span data-stu-id="55a3a-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="55a3a-137">Корпорация Майкрософт приостанавливает MyDW_DO_NOT_USE_[метка_времени].</span><span class="sxs-lookup"><span data-stu-id="55a3a-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="55a3a-138">В это время создается резервная копия.</span><span class="sxs-lookup"><span data-stu-id="55a3a-138">During this time, a backup is taken.</span></span> <span data-ttu-id="55a3a-139">Этот процесс может быть несколько раз приостановлен и возобновлен, если возникнут какие-либо проблемы.</span><span class="sxs-lookup"><span data-stu-id="55a3a-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="55a3a-140">Корпорация Майкрософт создает новое хранилище данных с именем «MyDW» в хранилище класса premium из резервной копии hello в шаге 2.</span><span class="sxs-lookup"><span data-stu-id="55a3a-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="55a3a-141">«MyDW» появятся только после завершения восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="55a3a-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="55a3a-142">После завершения восстановления hello, «MyDW» возвращает toohello и тех же данных в хранилище единицы и состоянии (или приостановлено), которое было до миграции hello.</span><span class="sxs-lookup"><span data-stu-id="55a3a-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="55a3a-143">После завершения миграции hello Майкрософт удалит «MyDW_DO_NOT_USE_ [Timestamp]».</span><span class="sxs-lookup"><span data-stu-id="55a3a-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="55a3a-144">Hello следующие параметры не переносятся в ходе миграции hello:</span><span class="sxs-lookup"><span data-stu-id="55a3a-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="55a3a-145">Аудит на уровне базы данных hello должен снова включить toobe.</span><span class="sxs-lookup"><span data-stu-id="55a3a-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="55a3a-146">Правила брандмауэра на уровне базы данных hello должны toobe повторно добавлены.</span><span class="sxs-lookup"><span data-stu-id="55a3a-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="55a3a-147">Правила брандмауэра на уровне сервера hello не затрагиваются.</span><span class="sxs-lookup"><span data-stu-id="55a3a-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="55a3a-148">расписание автоматического переноса</span><span class="sxs-lookup"><span data-stu-id="55a3a-148">Automatic migration schedule</span></span>
<span data-ttu-id="55a3a-149">Автоматическая миграция период между 6:00 и 6:00:00 (местное время в одном регионе) hello, после отключения расписания.</span><span class="sxs-lookup"><span data-stu-id="55a3a-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="55a3a-150">**Регион**</span><span class="sxs-lookup"><span data-stu-id="55a3a-150">**Region**</span></span> | <span data-ttu-id="55a3a-151">**Предполагаемая дата начала**</span><span class="sxs-lookup"><span data-stu-id="55a3a-151">**Estimated start date**</span></span> | <span data-ttu-id="55a3a-152">**Предполагаемая дата окончания**</span><span class="sxs-lookup"><span data-stu-id="55a3a-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="55a3a-153">Восточная часть Австралии</span><span class="sxs-lookup"><span data-stu-id="55a3a-153">Australia East</span></span> |<span data-ttu-id="55a3a-154">Еще не определено</span><span class="sxs-lookup"><span data-stu-id="55a3a-154">Not determined yet</span></span> |<span data-ttu-id="55a3a-155">Еще не определено</span><span class="sxs-lookup"><span data-stu-id="55a3a-155">Not determined yet</span></span> |
| <span data-ttu-id="55a3a-156">Восток Китая</span><span class="sxs-lookup"><span data-stu-id="55a3a-156">China East</span></span> |<span data-ttu-id="55a3a-157">9 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-157">January 9, 2017</span></span> |<span data-ttu-id="55a3a-158">13 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-158">January 13, 2017</span></span> |
| <span data-ttu-id="55a3a-159">Север Китая</span><span class="sxs-lookup"><span data-stu-id="55a3a-159">China North</span></span> |<span data-ttu-id="55a3a-160">9 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-160">January 9, 2017</span></span> |<span data-ttu-id="55a3a-161">13 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-161">January 13, 2017</span></span> |
| <span data-ttu-id="55a3a-162">Центральная Германия</span><span class="sxs-lookup"><span data-stu-id="55a3a-162">Germany Central</span></span> |<span data-ttu-id="55a3a-163">9 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-163">January 9, 2017</span></span> |<span data-ttu-id="55a3a-164">13 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-164">January 13, 2017</span></span> |
| <span data-ttu-id="55a3a-165">Северо-восточная Германия</span><span class="sxs-lookup"><span data-stu-id="55a3a-165">Germany Northeast</span></span> |<span data-ttu-id="55a3a-166">9 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-166">January 9, 2017</span></span> |<span data-ttu-id="55a3a-167">13 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-167">January 13, 2017</span></span> |
| <span data-ttu-id="55a3a-168">Западная Индия</span><span class="sxs-lookup"><span data-stu-id="55a3a-168">India West</span></span> |<span data-ttu-id="55a3a-169">Еще не определено</span><span class="sxs-lookup"><span data-stu-id="55a3a-169">Not determined yet</span></span> |<span data-ttu-id="55a3a-170">Еще не определено</span><span class="sxs-lookup"><span data-stu-id="55a3a-170">Not determined yet</span></span> |
| <span data-ttu-id="55a3a-171">Западная часть Японии</span><span class="sxs-lookup"><span data-stu-id="55a3a-171">Japan West</span></span> |<span data-ttu-id="55a3a-172">Еще не определено</span><span class="sxs-lookup"><span data-stu-id="55a3a-172">Not determined yet</span></span> |<span data-ttu-id="55a3a-173">Еще не определено</span><span class="sxs-lookup"><span data-stu-id="55a3a-173">Not determined yet</span></span> |
| <span data-ttu-id="55a3a-174">Северо-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="55a3a-174">North Central US</span></span> |<span data-ttu-id="55a3a-175">9 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-175">January 9, 2017</span></span> |<span data-ttu-id="55a3a-176">13 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="55a3a-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="55a3a-177">Хранилище toopremium самостоятельной миграции</span><span class="sxs-lookup"><span data-stu-id="55a3a-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="55a3a-178">Если требуется toocontrol, когда произойдет время простоя, можно использовать следующие шаги toomigrate существующее хранилище данных в стандартном хранилище toopremium хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="55a3a-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="55a3a-179">Если этот параметр выбран, hello самостоятельной миграции необходимо выполнить перед началом миграции автоматического hello в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="55a3a-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="55a3a-180">Это гарантирует, что позволяет избежать риска hello автоматическую миграцию, вызывающем конфликт (см. toohello [расписание автоматического переноса][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="55a3a-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="55a3a-181">Инструкции по самостоятельной миграции</span><span class="sxs-lookup"><span data-stu-id="55a3a-181">Self-migration instructions</span></span>
<span data-ttu-id="55a3a-182">toomigrate данные в хранилище самостоятельно, hello архивирования и восстановления использовать функции.</span><span class="sxs-lookup"><span data-stu-id="55a3a-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="55a3a-183">Hello восстановления миграции hello представлена ожидаемый tootake от часа за терабайт хранилища в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="55a3a-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="55a3a-184">Hello tookeep одинаковые имена, после завершения миграции, выполните hello [toorename действия во время миграции][steps toorename during migration].</span><span class="sxs-lookup"><span data-stu-id="55a3a-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="55a3a-185">[Приостановите работу][Pause] хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="55a3a-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="55a3a-186">При этом будет выполнено автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="55a3a-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="55a3a-187">[Восстановите][Restore] данные из последнего моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="55a3a-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="55a3a-188">Удалите имеющееся хранилище данных, размещенное в хранилище класса Standard.</span><span class="sxs-lookup"><span data-stu-id="55a3a-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="55a3a-189">**Если этот шаг не toodo, будет взиматься плата за обоих хранилищах данных.**</span><span class="sxs-lookup"><span data-stu-id="55a3a-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="55a3a-190">Hello следующие параметры не переносятся в ходе миграции hello:</span><span class="sxs-lookup"><span data-stu-id="55a3a-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="55a3a-191">Аудит на уровне базы данных hello должен снова включить toobe.</span><span class="sxs-lookup"><span data-stu-id="55a3a-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="55a3a-192">Правила брандмауэра на уровне базы данных hello должны toobe повторно добавлены.</span><span class="sxs-lookup"><span data-stu-id="55a3a-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="55a3a-193">Правила брандмауэра на уровне сервера hello не затрагиваются.</span><span class="sxs-lookup"><span data-stu-id="55a3a-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="55a3a-194">Переименуйте хранилище данных во время переноса (необязательно)</span><span class="sxs-lookup"><span data-stu-id="55a3a-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="55a3a-195">Две базы данных на hello на одном логическом сервере не может иметь hello таким же именем.</span><span class="sxs-lookup"><span data-stu-id="55a3a-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="55a3a-196">Хранилище данных SQL теперь поддерживает возможность hello toorename хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="55a3a-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="55a3a-197">В этом примере мы рассмотрим существующее хранилище данных с именем MyDW, размещенное в хранилище класса Standard.</span><span class="sxs-lookup"><span data-stu-id="55a3a-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="55a3a-198">Переименуйте «MyDW» hello, выполнив команду ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="55a3a-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="55a3a-199">(В этом примере мы будем переименованием «MyDW_BeforeMigration.»)  Эта команда останавливает все существующие транзакции и должна быть выполнена в toosucceed hello базы данных master.</span><span class="sxs-lookup"><span data-stu-id="55a3a-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="55a3a-200">[Приостановите работу][Pause] хранилища MyDW_BeforeMigration.</span><span class="sxs-lookup"><span data-stu-id="55a3a-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="55a3a-201">При этом будет выполнено автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="55a3a-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="55a3a-202">[Восстановление] [ Restore] из самый последний моментальный снимок новой базы данных с именем hello он используется toobe (например, «MyDW»).</span><span class="sxs-lookup"><span data-stu-id="55a3a-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="55a3a-203">Удалите хранилище данных MyDW_BeforeMigration.</span><span class="sxs-lookup"><span data-stu-id="55a3a-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="55a3a-204">**Если этот шаг не toodo, будет взиматься плата за обоих хранилищах данных.**</span><span class="sxs-lookup"><span data-stu-id="55a3a-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="55a3a-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55a3a-205">Next steps</span></span>
<span data-ttu-id="55a3a-206">С hello изменить toopremium хранилище, необходимо также создать требуется увеличение количества файлов больших двоичных объектов базы данных в hello базовой архитектуры хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="55a3a-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="55a3a-207">выигрыш в производительности hello toomaximize этого изменения перестройке кластеризованных индексов с помощью hello, выполнив сценарий.</span><span class="sxs-lookup"><span data-stu-id="55a3a-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="55a3a-208">Hello скрипт работает путем принудительного некоторые из существующих данных toohello дополнительных BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="55a3a-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="55a3a-209">Если не предпринимать никаких действий, данных Здравствуй естественным образом будет распространять со временем как загрузить дополнительные данные в таблицах.</span><span class="sxs-lookup"><span data-stu-id="55a3a-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="55a3a-210">**Предварительные требования:**</span><span class="sxs-lookup"><span data-stu-id="55a3a-210">**Prerequisites:**</span></span>

- <span data-ttu-id="55a3a-211">Hello хранилище данных следует запускать с единицами измерения хранилища данных 1000 или более поздней версии (в разделе [шкалы вычислительная мощность][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="55a3a-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="55a3a-212">Hello пользователь, выполняющий скрипт hello должно быть в hello [роли mediumrc] [ mediumrc role] или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="55a3a-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="55a3a-213">tooadd toothis роль пользователя выполнить hello ниже:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="55a3a-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="55a3a-214">Если возникли проблемы с хранилищу данных [создать обращение в службу поддержки] [ create a support ticket] и ссылаться на «хранилище миграции toopremium» как hello из возможных причин.</span><span class="sxs-lookup"><span data-stu-id="55a3a-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
