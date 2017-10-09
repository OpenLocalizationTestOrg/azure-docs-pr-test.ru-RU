---
title: "aaaAutoscaling и v1 среды службы приложений"
description: "Автоматическое масштабирование и среда службы приложений"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="7eef8-103">Автомасштабирование и среда службы приложений версии 1</span><span class="sxs-lookup"><span data-stu-id="7eef8-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="7eef8-104">Эта статья является о hello v1 среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="7eef8-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="7eef8-105">Имеется более новая версия hello среды службы приложений, удобнее toouse и выполняется на более мощный инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="7eef8-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="7eef8-106">Дополнительные сведения о новой версии hello начинаться с hello toolearn [toohello введение среды службы приложений](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="7eef8-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="7eef8-107">Среды службы приложений Azure поддерживают *автоматическое масштабирование*.</span><span class="sxs-lookup"><span data-stu-id="7eef8-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="7eef8-108">Вы можете настроить автоматическое масштабирование отдельных рабочих пулов на основе метрик или расписаний.</span><span class="sxs-lookup"><span data-stu-id="7eef8-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Параметры автоматического масштабирования для рабочего пула.][intro]

<span data-ttu-id="7eef8-110">Автоматическое масштабирование оптимизирует использование ресурсов, автоматическое увеличение и уменьшение toofit среды службы приложений профиль бюджете и нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7eef8-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment toofit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="7eef8-111">Настройка автоматического масштабирования рабочего пула</span><span class="sxs-lookup"><span data-stu-id="7eef8-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="7eef8-112">Функциональные возможности автоматического масштабирования hello доступны из hello **параметры** вкладке hello рабочего пула.</span><span class="sxs-lookup"><span data-stu-id="7eef8-112">You can access hello autoscale functionality from hello **Settings** tab of hello worker pool.</span></span>

![Вкладка "Параметры" hello рабочего пула.][settings-scale]

<span data-ttu-id="7eef8-114">После этого hello интерфейса должен быть достаточно ознакомиться с момента его планирование такие же возможности, которые вы видите, если масштабирование службы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7eef8-114">From there, hello interface should be fairly familiar since it is hello same experience that you see when you scale an App Service plan.</span></span> 

![Параметры масштабирования вручную.][scale-manual]

<span data-ttu-id="7eef8-116">Можно также настроить профиль автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="7eef8-116">You can also configure an autoscale profile.</span></span>

![Параметры автомасштабирования.][scale-profile]

<span data-ttu-id="7eef8-118">Профилей автомасштабирования являются полезным tooset ограничения на шкале.</span><span class="sxs-lookup"><span data-stu-id="7eef8-118">Autoscale profiles are useful tooset limits on your scale.</span></span> <span data-ttu-id="7eef8-119">Вы обеспечите согласованную производительность, установив значение нижней границы масштаба (1), а также прогнозируемый лимит затрат, установив значение верхней границы (2).</span><span class="sxs-lookup"><span data-stu-id="7eef8-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Параметры масштабирования в профиле.][scale-profile2]

<span data-ttu-id="7eef8-121">После определения профиля, можно добавить tooscale правила автоматического масштабирования вверх или вниз hello число экземпляров в пуле рабочих процессов hello в пределах границ hello, определяемые hello профилем.</span><span class="sxs-lookup"><span data-stu-id="7eef8-121">After you define a profile, you can add autoscale rules tooscale up or down hello number of instances in hello worker pool within hello bounds defined by hello profile.</span></span> <span data-ttu-id="7eef8-122">Правила автоматического масштабирования основаны на метриках.</span><span class="sxs-lookup"><span data-stu-id="7eef8-122">Autoscale rules are based on metrics.</span></span>

![Правило масштабирования.][scale-rule]

 <span data-ttu-id="7eef8-124">Любой рабочего пула или метрики интерфейса может быть используется toodefine правил автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="7eef8-124">Any worker pool or front-end metrics can be used toodefine autoscale rules.</span></span> <span data-ttu-id="7eef8-125">Эти метрики являются одинаковых метрик можно отслеживать в колонке графики hello ресурсов или задать предупреждения для приветствия.</span><span class="sxs-lookup"><span data-stu-id="7eef8-125">These metrics are hello same metrics you can monitor in hello resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="7eef8-126">Пример автоматического масштабирования</span><span class="sxs-lookup"><span data-stu-id="7eef8-126">Autoscale example</span></span>
<span data-ttu-id="7eef8-127">Автомасштабирование среды службы приложений лучше всего проиллюстрировать пошаговым сценарием.</span><span class="sxs-lookup"><span data-stu-id="7eef8-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="7eef8-128">В этой статье описываются все необходимые рекомендации hello при настройке автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="7eef8-128">This article explains all hello necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="7eef8-129">Hello статье рассматриваются hello воспроизведения взаимодействия, которые следует учитывать при вклад в автоматическом масштабировании среды службы приложений, размещенных в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="7eef8-129">hello article walks you through hello interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="7eef8-130">Общие сведения о сценарии</span><span class="sxs-lookup"><span data-stu-id="7eef8-130">Scenario introduction</span></span>
<span data-ttu-id="7eef8-131">Пользователь является членом роли sysadmin для предприятия, после завершения миграции часть hello рабочих нагрузок, которым он управляет tooan среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="7eef8-131">Frank is a sysadmin for an enterprise who has migrated a portion of hello workloads that he manages tooan App Service environment.</span></span>

<span data-ttu-id="7eef8-132">Hello среды службы приложений масштаба toomanual следующую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="7eef8-132">hello App Service environment is configured toomanual scale as follows:</span></span>

* <span data-ttu-id="7eef8-133">**внешние интерфейсы** : 3;</span><span class="sxs-lookup"><span data-stu-id="7eef8-133">**Front ends:** 3</span></span>
* <span data-ttu-id="7eef8-134">**рабочий пул 1**: 10;</span><span class="sxs-lookup"><span data-stu-id="7eef8-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="7eef8-135">**рабочий пул 2**: 5;</span><span class="sxs-lookup"><span data-stu-id="7eef8-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="7eef8-136">**рабочий пул 3**: 5.</span><span class="sxs-lookup"><span data-stu-id="7eef8-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="7eef8-137">Рабочий пул 1 используется для производственных рабочих нагрузок, а рабочий пул 2 и рабочий пул 3 — для задач контроля качества и разработки.</span><span class="sxs-lookup"><span data-stu-id="7eef8-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="7eef8-138">Hello приложения планы обслуживания для контроля Качества и разработки можно настроить toomanual шкалы.</span><span class="sxs-lookup"><span data-stu-id="7eef8-138">hello App Service plans for QA and dev are configured toomanual scale.</span></span> <span data-ttu-id="7eef8-139">Hello производственного плана служб приложений задается toodeal tooautoscale с вариациями нагрузку и трафик.</span><span class="sxs-lookup"><span data-stu-id="7eef8-139">hello production App Service plan is set tooautoscale toodeal with variations in load and traffic.</span></span>

<span data-ttu-id="7eef8-140">Федор хорошо знакомы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7eef8-140">Frank is very familiar with hello application.</span></span> <span data-ttu-id="7eef8-141">Он знает, что hello часы максимальной нагрузки для нагрузочных являются между 9:00:00 и 18:00:00, так как это бизнес приложения (LOB), сотрудники используют, когда они находятся в офисе hello.</span><span class="sxs-lookup"><span data-stu-id="7eef8-141">He knows that hello peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in hello office.</span></span> <span data-ttu-id="7eef8-142">В конце рабочего дня показатели использования падают.</span><span class="sxs-lookup"><span data-stu-id="7eef8-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="7eef8-143">За пределами часы максимальной нагрузки по-прежнему повышению нагрузки, так как пользователям приложение hello удаленно с помощью своих мобильных устройств или домашние компьютеры.</span><span class="sxs-lookup"><span data-stu-id="7eef8-143">Outside peak hours, there is still some load because users can access hello app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="7eef8-144">Hello производственного плана служб приложений уже настроены tooautoscale, в зависимости от использования ЦП с hello правилам:</span><span class="sxs-lookup"><span data-stu-id="7eef8-144">hello production App Service plan is already configured tooautoscale based on CPU usage with hello following rules:</span></span>

![Параметры бизнес-приложения.][asp-scale]

| <span data-ttu-id="7eef8-146">**Профиль автоматического масштабирования — рабочие дни — план службы приложений**</span><span class="sxs-lookup"><span data-stu-id="7eef8-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="7eef8-147">**Профиль автоматического масштабирования — выходные дни — план службы приложений**</span><span class="sxs-lookup"><span data-stu-id="7eef8-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="7eef8-148">**Имя:** профиль рабочего дня</span><span class="sxs-lookup"><span data-stu-id="7eef8-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="7eef8-149">**Имя:** профиль выходного дня</span><span class="sxs-lookup"><span data-stu-id="7eef8-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="7eef8-150">**Масштабирование:** расписание и правила производительности</span><span class="sxs-lookup"><span data-stu-id="7eef8-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="7eef8-151">**Масштабирование:** расписание и правила производительности</span><span class="sxs-lookup"><span data-stu-id="7eef8-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="7eef8-152">**Профиль:** рабочие дни</span><span class="sxs-lookup"><span data-stu-id="7eef8-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="7eef8-153">**Профиль:** выходные дни</span><span class="sxs-lookup"><span data-stu-id="7eef8-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="7eef8-154">**Тип:** повторение</span><span class="sxs-lookup"><span data-stu-id="7eef8-154">**Type:** Recurrence</span></span> |<span data-ttu-id="7eef8-155">**Тип:** повторение</span><span class="sxs-lookup"><span data-stu-id="7eef8-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="7eef8-156">**Целевой диапазон:** 5 экземпляров too20</span><span class="sxs-lookup"><span data-stu-id="7eef8-156">**Target range:** 5 too20 instances</span></span> |<span data-ttu-id="7eef8-157">**Целевой диапазон:** 3 too10 экземпляров</span><span class="sxs-lookup"><span data-stu-id="7eef8-157">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="7eef8-158">**Дни:** понедельник, вторник, среда, четверг, пятница</span><span class="sxs-lookup"><span data-stu-id="7eef8-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="7eef8-159">**Дни:** суббота, воскресенье</span><span class="sxs-lookup"><span data-stu-id="7eef8-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="7eef8-160">**Время начала:** 9:00</span><span class="sxs-lookup"><span data-stu-id="7eef8-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="7eef8-161">**Время начала:** 9:00</span><span class="sxs-lookup"><span data-stu-id="7eef8-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="7eef8-162">**Часовой пояс:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="7eef8-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="7eef8-163">**Часовой пояс:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="7eef8-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="7eef8-164">**Правило автоматического масштабирования (увеличение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="7eef8-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="7eef8-165">**Правило автоматического масштабирования (увеличение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="7eef8-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="7eef8-166">**Ресурс:** производство (среда службы приложений)</span><span class="sxs-lookup"><span data-stu-id="7eef8-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="7eef8-167">**Ресурс:** производство (среда службы приложений)</span><span class="sxs-lookup"><span data-stu-id="7eef8-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="7eef8-168">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="7eef8-168">**Metric:** CPU %</span></span> |<span data-ttu-id="7eef8-169">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="7eef8-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="7eef8-170">**Операции:** более 60 %</span><span class="sxs-lookup"><span data-stu-id="7eef8-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="7eef8-171">**Операции:** более 80 %</span><span class="sxs-lookup"><span data-stu-id="7eef8-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="7eef8-172">**Длительность:** 5 минут</span><span class="sxs-lookup"><span data-stu-id="7eef8-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="7eef8-173">**Длительность:** 10 минут</span><span class="sxs-lookup"><span data-stu-id="7eef8-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="7eef8-174">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="7eef8-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="7eef8-175">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="7eef8-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="7eef8-176">**Действие:** увеличить количество на 2</span><span class="sxs-lookup"><span data-stu-id="7eef8-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="7eef8-177">**Действие:** увеличить количество на 1</span><span class="sxs-lookup"><span data-stu-id="7eef8-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="7eef8-178">**Охлаждение (в минутах):** 15</span><span class="sxs-lookup"><span data-stu-id="7eef8-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="7eef8-179">**Охлаждение (в минутах):** 20</span><span class="sxs-lookup"><span data-stu-id="7eef8-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="7eef8-180">**Правило автоматического масштабирования (уменьшение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="7eef8-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="7eef8-181">**Правило автоматического масштабирования (уменьшение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="7eef8-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="7eef8-182">**Ресурс:** производство (среда службы приложений)</span><span class="sxs-lookup"><span data-stu-id="7eef8-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="7eef8-183">**Ресурс:** производство (среда службы приложений)</span><span class="sxs-lookup"><span data-stu-id="7eef8-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="7eef8-184">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="7eef8-184">**Metric:** CPU %</span></span> |<span data-ttu-id="7eef8-185">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="7eef8-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="7eef8-186">**Операции:** менее 30 %</span><span class="sxs-lookup"><span data-stu-id="7eef8-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="7eef8-187">**Операции:** менее 20 %</span><span class="sxs-lookup"><span data-stu-id="7eef8-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="7eef8-188">**Длительность:** 10 минут</span><span class="sxs-lookup"><span data-stu-id="7eef8-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="7eef8-189">**Длительность:** 15 минут</span><span class="sxs-lookup"><span data-stu-id="7eef8-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="7eef8-190">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="7eef8-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="7eef8-191">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="7eef8-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="7eef8-192">**Действие:** уменьшить количество на 1</span><span class="sxs-lookup"><span data-stu-id="7eef8-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="7eef8-193">**Действие:** уменьшить количество на 1</span><span class="sxs-lookup"><span data-stu-id="7eef8-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="7eef8-194">**Охлаждение (в минутах):** 20</span><span class="sxs-lookup"><span data-stu-id="7eef8-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="7eef8-195">**Охлаждение (в минутах):** 10</span><span class="sxs-lookup"><span data-stu-id="7eef8-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="7eef8-196">Скорость роста плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="7eef8-196">App Service plan inflation rate</span></span>
<span data-ttu-id="7eef8-197">Планы служб приложений, настроенных tooautoscale сделать это с максимальной скоростью в час.</span><span class="sxs-lookup"><span data-stu-id="7eef8-197">App Service plans that are configured tooautoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="7eef8-198">Эту частоту можно вычислить на основе hello значения, указанные в правиле автоматического масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="7eef8-198">This rate can be calculated based on hello values provided on hello autoscale rule.</span></span>

<span data-ttu-id="7eef8-199">Основные сведения о и вычисления hello *скорость расширению плана служб приложений* важно для автоматического масштабирования среды службы приложений, так как пул рабочих tooa изменения масштаба не мгновенно.</span><span class="sxs-lookup"><span data-stu-id="7eef8-199">Understanding and calculating hello *App Service plan inflation rate* is important for App Service environment autoscale because scale changes tooa worker pool are not instantaneous.</span></span>

<span data-ttu-id="7eef8-200">Hello скорость расширению плана служб приложений вычисляется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7eef8-200">hello App Service plan inflation rate is calculated as follows:</span></span>

![Расчет скорости роста плана службы приложений.][ASP-Inflation]

<span data-ttu-id="7eef8-202">В основе hello автомасштабирования — правило масштабирования вверх для профиля Weekday hello hello производства план служб приложений:</span><span class="sxs-lookup"><span data-stu-id="7eef8-202">Based on hello Autoscale – Scale Up rule for hello Weekday profile of hello production App Service plan:</span></span>

![Скорость роста плана службы приложений для рабочих дней на основе правила "Автомасштабирование — увеличение масштаба".][Equation1]

<span data-ttu-id="7eef8-204">В случае, когда hello hello автомасштабирования — правило масштабирования вверх для профиля hello выходные дни производства hello план служб приложений формула hello разрешится:</span><span class="sxs-lookup"><span data-stu-id="7eef8-204">In hello case of hello Autoscale – Scale Up rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>

![Скорость роста плана службы приложений для выходных дней на основе правила "Автомасштабирование — увеличение масштаба".][Equation2]

<span data-ttu-id="7eef8-206">Это значение можно вычислить и для операций уменьшения масштаба.</span><span class="sxs-lookup"><span data-stu-id="7eef8-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="7eef8-207">Зависимости hello автомасштабирования — правило масштабирования вниз для профиля Weekday hello hello производства план служб приложений, это будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7eef8-207">Based on hello Autoscale – Scale Down rule for hello Weekday profile of hello production App Service plan, this would look as follows:</span></span>

![Скорость роста плана службы приложений для рабочих дней на основе правила "Автомасштабирование — уменьшение масштаба".][Equation3]

<span data-ttu-id="7eef8-209">В случае, когда hello hello автомасштабирования — правило масштабирования вниз для профиля hello выходные дни производства hello план служб приложений формула hello разрешится:</span><span class="sxs-lookup"><span data-stu-id="7eef8-209">In hello case of hello Autoscale – Scale Down rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>  

![Скорость роста плана службы приложений для выходных дней на основе правила "Автомасштабирование — уменьшение масштаба".][Equation4]

<span data-ttu-id="7eef8-211">Hello производственного плана служб приложений могут увеличиваться на максимальной скорости в восьми экземпляров в час за неделю hello и четырех экземпляров в час hello выходные дни.</span><span class="sxs-lookup"><span data-stu-id="7eef8-211">hello production App Service plan can grow at a maximum rate of eight instances/hour during hello week and four instances/hour during hello weekend.</span></span> <span data-ttu-id="7eef8-212">Его можно освободить экземпляры с максимальной скоростью четырех экземпляров в час за неделю hello и шести экземпляров в час в выходные дни.</span><span class="sxs-lookup"><span data-stu-id="7eef8-212">It can release instances at a maximum rate of four instances/hour during hello week and six instances/hour during weekends.</span></span>

<span data-ttu-id="7eef8-213">Если несколько планов служб приложений размещаются в пуле рабочего процесса, у вас есть toocalculate hello *общая скорость расширению* как сумма hello hello расширению скорость для всех hello планы службы приложений, которые размещения в этом пуле рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="7eef8-213">If multiple App Service plans are being hosted in a worker pool, you have toocalculate hello *total inflation rate* as hello sum of hello inflation rate for all hello App Service plans that are being hosting in that worker pool.</span></span>

![Расчет общей скорости роста по нескольким планам службы приложений, размещенным в рабочем пуле.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a><span data-ttu-id="7eef8-215">Правил автомасштабирования пула рабочих toodefine скорость расширению планирование hello использования службы приложений</span><span class="sxs-lookup"><span data-stu-id="7eef8-215">Use hello App Service plan inflation rate toodefine worker pool autoscale rules</span></span>
<span data-ttu-id="7eef8-216">Рабочих пулов, на которых размещены планы служб приложений, настроенных tooautoscale нужно выделить буфер емкости.</span><span class="sxs-lookup"><span data-stu-id="7eef8-216">Worker pools that host App Service plans that are configured tooautoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="7eef8-217">буфер Hello обеспечивает toogrow операций автомасштабирования hello и сжатие план служб приложений, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="7eef8-217">hello buffer allows for hello autoscale operations toogrow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="7eef8-218">Минимальное буфера Hello бы, что hello вычисляется общее приложение службы планирования расширению скорость.</span><span class="sxs-lookup"><span data-stu-id="7eef8-218">hello minimum buffer would be hello calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="7eef8-219">Операции масштабирования среды службы приложений занять некоторое время tooapply, любое изменение следует учитывать для дальнейших изменений запросу, может произойти во время операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="7eef8-219">Because App Service environment scale operations take some time tooapply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="7eef8-220">tooaccommodate такой задержкой, рекомендуется использовать hello вычисляется общее приложение службы планирования расширению скорость как hello минимальное число экземпляров, которые добавляются для каждой операции автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="7eef8-220">tooaccommodate this latency, we recommend that you use hello calculated Total App Service Plan Inflation Rate as hello minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="7eef8-221">С этой информацией Михаил можно определить hello профиль автомасштабирования и правила:</span><span class="sxs-lookup"><span data-stu-id="7eef8-221">With this information, Frank can define hello following autoscale profile and rules:</span></span>

![Правила профиля автомасштабирования на примере бизнес-приложения.][Worker-Pool-Scale]

| <span data-ttu-id="7eef8-223">**Профиль автоматического масштабирования — рабочие дни**</span><span class="sxs-lookup"><span data-stu-id="7eef8-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="7eef8-224">**Профиль автоматического масштабирования — выходные дни**</span><span class="sxs-lookup"><span data-stu-id="7eef8-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="7eef8-225">**Имя:** профиль рабочего дня</span><span class="sxs-lookup"><span data-stu-id="7eef8-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="7eef8-226">**Имя:** профиль выходного дня</span><span class="sxs-lookup"><span data-stu-id="7eef8-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="7eef8-227">**Масштабирование:** расписание и правила производительности</span><span class="sxs-lookup"><span data-stu-id="7eef8-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="7eef8-228">**Масштабирование:** расписание и правила производительности</span><span class="sxs-lookup"><span data-stu-id="7eef8-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="7eef8-229">**Профиль:** рабочие дни</span><span class="sxs-lookup"><span data-stu-id="7eef8-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="7eef8-230">**Профиль:** выходные дни</span><span class="sxs-lookup"><span data-stu-id="7eef8-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="7eef8-231">**Тип:** повторение</span><span class="sxs-lookup"><span data-stu-id="7eef8-231">**Type:** Recurrence</span></span> |<span data-ttu-id="7eef8-232">**Тип:** повторение</span><span class="sxs-lookup"><span data-stu-id="7eef8-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="7eef8-233">**Целевой диапазон:** 13 too25 экземпляров</span><span class="sxs-lookup"><span data-stu-id="7eef8-233">**Target range:** 13 too25 instances</span></span> |<span data-ttu-id="7eef8-234">**Целевой диапазон:** 6 экземпляров too15</span><span class="sxs-lookup"><span data-stu-id="7eef8-234">**Target range:** 6 too15 instances</span></span> |
| <span data-ttu-id="7eef8-235">**Дни:** понедельник, вторник, среда, четверг, пятница</span><span class="sxs-lookup"><span data-stu-id="7eef8-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="7eef8-236">**Дни:** суббота, воскресенье</span><span class="sxs-lookup"><span data-stu-id="7eef8-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="7eef8-237">**Время начала:** 7:00</span><span class="sxs-lookup"><span data-stu-id="7eef8-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="7eef8-238">**Время начала:** 9:00</span><span class="sxs-lookup"><span data-stu-id="7eef8-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="7eef8-239">**Часовой пояс:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="7eef8-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="7eef8-240">**Часовой пояс:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="7eef8-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="7eef8-241">**Правило автоматического масштабирования (увеличение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="7eef8-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="7eef8-242">**Правило автоматического масштабирования (увеличение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="7eef8-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="7eef8-243">**Ресурс:** рабочий пул 1</span><span class="sxs-lookup"><span data-stu-id="7eef8-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="7eef8-244">**Ресурс:** рабочий пул 1</span><span class="sxs-lookup"><span data-stu-id="7eef8-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="7eef8-245">**Метрика:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="7eef8-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="7eef8-246">**Метрика:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="7eef8-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="7eef8-247">**Операции:** менее 8</span><span class="sxs-lookup"><span data-stu-id="7eef8-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="7eef8-248">**Операции:** менее 3</span><span class="sxs-lookup"><span data-stu-id="7eef8-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="7eef8-249">**Длительность:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="7eef8-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="7eef8-250">**Длительность:** 30 минут</span><span class="sxs-lookup"><span data-stu-id="7eef8-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="7eef8-251">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="7eef8-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="7eef8-252">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="7eef8-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="7eef8-253">**Действие:** увеличить количество на 8</span><span class="sxs-lookup"><span data-stu-id="7eef8-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="7eef8-254">**Действие:** увеличить количество на 3</span><span class="sxs-lookup"><span data-stu-id="7eef8-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="7eef8-255">**Охлаждение (в минутах):** 180</span><span class="sxs-lookup"><span data-stu-id="7eef8-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="7eef8-256">**Охлаждение (в минутах):** 180</span><span class="sxs-lookup"><span data-stu-id="7eef8-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="7eef8-257">**Правило автоматического масштабирования (уменьшение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="7eef8-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="7eef8-258">**Правило автоматического масштабирования (уменьшение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="7eef8-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="7eef8-259">**Ресурс:** рабочий пул 1</span><span class="sxs-lookup"><span data-stu-id="7eef8-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="7eef8-260">**Ресурс:** рабочий пул 1</span><span class="sxs-lookup"><span data-stu-id="7eef8-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="7eef8-261">**Метрика:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="7eef8-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="7eef8-262">**Метрика:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="7eef8-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="7eef8-263">**Операции:** более 8</span><span class="sxs-lookup"><span data-stu-id="7eef8-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="7eef8-264">**Операции:** более 3</span><span class="sxs-lookup"><span data-stu-id="7eef8-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="7eef8-265">**Длительность:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="7eef8-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="7eef8-266">**Длительность:** 15 минут</span><span class="sxs-lookup"><span data-stu-id="7eef8-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="7eef8-267">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="7eef8-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="7eef8-268">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="7eef8-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="7eef8-269">**Действие:** уменьшить количество на 2</span><span class="sxs-lookup"><span data-stu-id="7eef8-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="7eef8-270">**Действие:** уменьшить количество на 3</span><span class="sxs-lookup"><span data-stu-id="7eef8-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="7eef8-271">**Охлаждение (в минутах):** 120</span><span class="sxs-lookup"><span data-stu-id="7eef8-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="7eef8-272">**Охлаждение (в минутах):** 120</span><span class="sxs-lookup"><span data-stu-id="7eef8-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="7eef8-273">Целевой диапазон, определенные в профиле hello Hello вычисляется путем hello минимальное экземпляров, определенные в профиль для hello план служб приложений + буфера.</span><span class="sxs-lookup"><span data-stu-id="7eef8-273">hello Target range defined in hello profile is calculated by hello minimum instances defined in the profile for hello App Service plan + buffer.</span></span>

<span data-ttu-id="7eef8-274">Максимальный диапазон Hello бы hello сумма всех hello максимального диапазонов все планы служб приложений, размещенных в пуле рабочих процессов hello.</span><span class="sxs-lookup"><span data-stu-id="7eef8-274">hello Maximum range would be hello sum of all hello maximum ranges for all App Service plans hosted in hello worker pool.</span></span>

<span data-ttu-id="7eef8-275">Hello увеличение числа для масштабирования hello правила следует tooat набор хотя бы один X ставка расширению план службы приложений для масштабирования вверх.</span><span class="sxs-lookup"><span data-stu-id="7eef8-275">hello Increase count for hello scale up rules should be set tooat least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="7eef8-276">Уменьшите число может быть скорректированное toosomething между 1/2 X или 1 X hello скорость расширению план службы приложений для масштабирования вниз.</span><span class="sxs-lookup"><span data-stu-id="7eef8-276">Decrease count can be adjusted toosomething between 1/2X or 1X hello App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="7eef8-277">Автоматическое масштабирование для интерфейсного пула</span><span class="sxs-lookup"><span data-stu-id="7eef8-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="7eef8-278">Правила автомасштабирования для интерфейсных пулов проще, чем правила для рабочих пулов.</span><span class="sxs-lookup"><span data-stu-id="7eef8-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="7eef8-279">Важно,</span><span class="sxs-lookup"><span data-stu-id="7eef8-279">Primarily, you should</span></span>  
<span data-ttu-id="7eef8-280">Убедитесь в том, продолжительность измерения hello и таймеры cooldown hello учитывать операций масштабирования в план служб приложений не отображаются мгновенно.</span><span class="sxs-lookup"><span data-stu-id="7eef8-280">make sure that duration of hello measurement and hello cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="7eef8-281">В этом сценарии Федор знает частота возникновения ошибок hello увеличивается, обслуживающих клиентские запросы по достижении 80% ресурсов ЦП и задает экземпляров tooincrease правила автомасштабирования hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7eef8-281">For this scenario, Frank knows that hello error rate increases after front ends reach 80% CPU utilization and sets hello autoscale rule tooincrease instances as follows:</span></span>

![Параметры автомасштабирования для интерфейсного пула.][Front-End-Scale]

| <span data-ttu-id="7eef8-283">**Профиль автоматического масштабирования — внешние интерфейсы**</span><span class="sxs-lookup"><span data-stu-id="7eef8-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="7eef8-284">**Имя:** автоматическое масштабирование — внешние интерфейсы</span><span class="sxs-lookup"><span data-stu-id="7eef8-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="7eef8-285">**Масштабирование:** расписание и правила производительности</span><span class="sxs-lookup"><span data-stu-id="7eef8-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="7eef8-286">**Профиль:** ежедневно</span><span class="sxs-lookup"><span data-stu-id="7eef8-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="7eef8-287">**Тип:** повторение</span><span class="sxs-lookup"><span data-stu-id="7eef8-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="7eef8-288">**Целевой диапазон:** 3 too10 экземпляров</span><span class="sxs-lookup"><span data-stu-id="7eef8-288">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="7eef8-289">**Дни:** ежедневно</span><span class="sxs-lookup"><span data-stu-id="7eef8-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="7eef8-290">**Время начала:** 9:00</span><span class="sxs-lookup"><span data-stu-id="7eef8-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="7eef8-291">**Часовой пояс:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="7eef8-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="7eef8-292">**Правило автоматического масштабирования (увеличение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="7eef8-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="7eef8-293">**Ресурс:** пул внешних интерфейсов</span><span class="sxs-lookup"><span data-stu-id="7eef8-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="7eef8-294">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="7eef8-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="7eef8-295">**Операции:** более 60 %</span><span class="sxs-lookup"><span data-stu-id="7eef8-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="7eef8-296">**Длительность:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="7eef8-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="7eef8-297">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="7eef8-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="7eef8-298">**Действие:** увеличить количество на 3</span><span class="sxs-lookup"><span data-stu-id="7eef8-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="7eef8-299">**Охлаждение (в минутах):** 120</span><span class="sxs-lookup"><span data-stu-id="7eef8-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="7eef8-300">**Правило автоматического масштабирования (уменьшение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="7eef8-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="7eef8-301">**Ресурс:** рабочий пул 1</span><span class="sxs-lookup"><span data-stu-id="7eef8-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="7eef8-302">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="7eef8-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="7eef8-303">**Операции:** менее 30 %</span><span class="sxs-lookup"><span data-stu-id="7eef8-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="7eef8-304">**Длительность:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="7eef8-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="7eef8-305">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="7eef8-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="7eef8-306">**Действие:** уменьшить количество на 3</span><span class="sxs-lookup"><span data-stu-id="7eef8-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="7eef8-307">**Охлаждение (в минутах):** 120</span><span class="sxs-lookup"><span data-stu-id="7eef8-307">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
