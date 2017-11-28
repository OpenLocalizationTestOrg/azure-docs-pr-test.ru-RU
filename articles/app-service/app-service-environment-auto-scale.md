---
title: "Автомасштабирование и среда службы приложений версии 1"
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
ms.openlocfilehash: f32affd285f3918feb0e893543f2a28f678b7b10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="5f6ac-103">Автомасштабирование и среда службы приложений версии 1</span><span class="sxs-lookup"><span data-stu-id="5f6ac-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="5f6ac-104">Эта статья посвящена среде службы приложений версии 1.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="5f6ac-105">Имеется более новая версия среды службы приложений, которая проще в использовании и которая работает на более мощной инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="5f6ac-106">Чтобы узнать больше о новой версии, начните с изучения статьи [Введение в среду службы приложения](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="5f6ac-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="5f6ac-107">Среды службы приложений Azure поддерживают *автоматическое масштабирование*.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="5f6ac-108">Вы можете настроить автоматическое масштабирование отдельных рабочих пулов на основе метрик или расписаний.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Параметры автоматического масштабирования для рабочего пула.][intro]

<span data-ttu-id="5f6ac-110">Автоматическое масштабирование оптимизирует использование ресурсов, без вашего участия увеличивая и уменьшая среду службы приложений с учетом бюджета и (или) профиля нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="5f6ac-111">Настройка автоматического масштабирования рабочего пула</span><span class="sxs-lookup"><span data-stu-id="5f6ac-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="5f6ac-112">Управлять автоматическим масштабированием можно на вкладке **Параметры** для рабочего пула.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-112">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span></span>

![Вкладка "Параметры" для рабочего пула.][settings-scale]

<span data-ttu-id="5f6ac-114">Этот интерфейс должен быть вам уже знаком — точно такой же используется при масштабировании плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-114">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span></span> 

![Параметры масштабирования вручную.][scale-manual]

<span data-ttu-id="5f6ac-116">Можно также настроить профиль автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-116">You can also configure an autoscale profile.</span></span>

![Параметры автомасштабирования.][scale-profile]

<span data-ttu-id="5f6ac-118">Профили автомасштабирования используются для настройки ограничений масштаба.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-118">Autoscale profiles are useful to set limits on your scale.</span></span> <span data-ttu-id="5f6ac-119">Вы обеспечите согласованную производительность, установив значение нижней границы масштаба (1), а также прогнозируемый лимит затрат, установив значение верхней границы (2).</span><span class="sxs-lookup"><span data-stu-id="5f6ac-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Параметры масштабирования в профиле.][scale-profile2]

<span data-ttu-id="5f6ac-121">Определив профиль, вы можете добавить правила автоматического масштабирования для увеличения или уменьшения числа экземпляров в рабочем пуле в пределах границ, определяемых профилем.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-121">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span></span> <span data-ttu-id="5f6ac-122">Правила автоматического масштабирования основаны на метриках.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-122">Autoscale rules are based on metrics.</span></span>

![Правило масштабирования.][scale-rule]

 <span data-ttu-id="5f6ac-124">Чтобы определить правила автомасштабирования, можно использовать любые метрики рабочего пула или внешнего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-124">Any worker pool or front-end metrics can be used to define autoscale rules.</span></span> <span data-ttu-id="5f6ac-125">Это те же метрики, которые можно отслеживать на графиках в колонке ресурсов и для которых можно настраивать оповещения.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-125">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="5f6ac-126">Пример автоматического масштабирования</span><span class="sxs-lookup"><span data-stu-id="5f6ac-126">Autoscale example</span></span>
<span data-ttu-id="5f6ac-127">Автомасштабирование среды службы приложений лучше всего проиллюстрировать пошаговым сценарием.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="5f6ac-128">В этой статье приведены все рекомендации, которые необходимо учитывать при настройке автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-128">This article explains all the necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="5f6ac-129">В ней рассматриваются все действия, которые выполняются при планировании автомасштабирования сред службы приложений, размещенных в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-129">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="5f6ac-130">Общие сведения о сценарии</span><span class="sxs-lookup"><span data-stu-id="5f6ac-130">Scenario introduction</span></span>
<span data-ttu-id="5f6ac-131">Федор — системный администратор предприятия, который перенес часть рабочих нагрузок в среду службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-131">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span></span>

<span data-ttu-id="5f6ac-132">Для этой среды службы приложений масштабирование вручную настроено так:</span><span class="sxs-lookup"><span data-stu-id="5f6ac-132">The App Service environment is configured to manual scale as follows:</span></span>

* <span data-ttu-id="5f6ac-133">**внешние интерфейсы** : 3;</span><span class="sxs-lookup"><span data-stu-id="5f6ac-133">**Front ends:** 3</span></span>
* <span data-ttu-id="5f6ac-134">**рабочий пул 1**: 10;</span><span class="sxs-lookup"><span data-stu-id="5f6ac-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="5f6ac-135">**рабочий пул 2**: 5;</span><span class="sxs-lookup"><span data-stu-id="5f6ac-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="5f6ac-136">**рабочий пул 3**: 5.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="5f6ac-137">Рабочий пул 1 используется для производственных рабочих нагрузок, а рабочий пул 2 и рабочий пул 3 — для задач контроля качества и разработки.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="5f6ac-138">Планы службы приложений для контроля качества и разработки настроены на ручное масштабирование.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-138">The App Service plans for QA and dev are configured to manual scale.</span></span> <span data-ttu-id="5f6ac-139">Для производственного плана службы приложений настроено автомасштабирование. Это помогает справляться с колебаниями нагрузки и трафика.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-139">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span></span>

<span data-ttu-id="5f6ac-140">Федор хорошо знаком с приложением.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-140">Frank is very familiar with the application.</span></span> <span data-ttu-id="5f6ac-141">Он знает, что пиковая нагрузка приходится на период с 9:00 до 18:00, ведь это бизнес-приложение используется сотрудниками, работающими в офисе.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-141">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span></span> <span data-ttu-id="5f6ac-142">В конце рабочего дня показатели использования падают.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="5f6ac-143">В этот период сохраняется некоторая рабочая нагрузка, так как пользователи могут использовать приложение удаленно с мобильных устройств или домашних компьютеров.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-143">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="5f6ac-144">Производственный план службы приложений уже настроен на автоматическое масштабирование в соответствии с загрузкой ЦП и на основе следующих правил:</span><span class="sxs-lookup"><span data-stu-id="5f6ac-144">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span></span>

![Параметры бизнес-приложения.][asp-scale]

| <span data-ttu-id="5f6ac-146">**Профиль автоматического масштабирования — рабочие дни — план службы приложений**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="5f6ac-147">**Профиль автоматического масштабирования — выходные дни — план службы приложений**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="5f6ac-148">**Имя:** профиль рабочего дня</span><span class="sxs-lookup"><span data-stu-id="5f6ac-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="5f6ac-149">**Имя:** профиль выходного дня</span><span class="sxs-lookup"><span data-stu-id="5f6ac-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="5f6ac-150">**Масштабирование:** расписание и правила производительности</span><span class="sxs-lookup"><span data-stu-id="5f6ac-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="5f6ac-151">**Масштабирование:** расписание и правила производительности</span><span class="sxs-lookup"><span data-stu-id="5f6ac-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="5f6ac-152">**Профиль:** рабочие дни</span><span class="sxs-lookup"><span data-stu-id="5f6ac-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="5f6ac-153">**Профиль:** выходные дни</span><span class="sxs-lookup"><span data-stu-id="5f6ac-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="5f6ac-154">**Тип:** повторение</span><span class="sxs-lookup"><span data-stu-id="5f6ac-154">**Type:** Recurrence</span></span> |<span data-ttu-id="5f6ac-155">**Тип:** повторение</span><span class="sxs-lookup"><span data-stu-id="5f6ac-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="5f6ac-156">**Целевой диапазон:** 5–20 экземпляров</span><span class="sxs-lookup"><span data-stu-id="5f6ac-156">**Target range:** 5 to 20 instances</span></span> |<span data-ttu-id="5f6ac-157">**Целевой диапазон:** 3–10 экземпляров</span><span class="sxs-lookup"><span data-stu-id="5f6ac-157">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="5f6ac-158">**Дни:** понедельник, вторник, среда, четверг, пятница</span><span class="sxs-lookup"><span data-stu-id="5f6ac-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="5f6ac-159">**Дни:** суббота, воскресенье</span><span class="sxs-lookup"><span data-stu-id="5f6ac-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="5f6ac-160">**Время начала:** 9:00</span><span class="sxs-lookup"><span data-stu-id="5f6ac-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="5f6ac-161">**Время начала:** 9:00</span><span class="sxs-lookup"><span data-stu-id="5f6ac-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="5f6ac-162">**Часовой пояс:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="5f6ac-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="5f6ac-163">**Часовой пояс:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="5f6ac-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="5f6ac-164">**Правило автоматического масштабирования (увеличение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="5f6ac-165">**Правило автоматического масштабирования (увеличение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="5f6ac-166">**Ресурс:** производство (среда службы приложений)</span><span class="sxs-lookup"><span data-stu-id="5f6ac-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="5f6ac-167">**Ресурс:** производство (среда службы приложений)</span><span class="sxs-lookup"><span data-stu-id="5f6ac-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="5f6ac-168">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="5f6ac-168">**Metric:** CPU %</span></span> |<span data-ttu-id="5f6ac-169">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="5f6ac-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="5f6ac-170">**Операции:** более 60 %</span><span class="sxs-lookup"><span data-stu-id="5f6ac-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="5f6ac-171">**Операции:** более 80 %</span><span class="sxs-lookup"><span data-stu-id="5f6ac-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="5f6ac-172">**Длительность:** 5 минут</span><span class="sxs-lookup"><span data-stu-id="5f6ac-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="5f6ac-173">**Длительность:** 10 минут</span><span class="sxs-lookup"><span data-stu-id="5f6ac-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="5f6ac-174">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="5f6ac-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="5f6ac-175">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="5f6ac-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="5f6ac-176">**Действие:** увеличить количество на 2</span><span class="sxs-lookup"><span data-stu-id="5f6ac-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="5f6ac-177">**Действие:** увеличить количество на 1</span><span class="sxs-lookup"><span data-stu-id="5f6ac-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="5f6ac-178">**Охлаждение (в минутах):** 15</span><span class="sxs-lookup"><span data-stu-id="5f6ac-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="5f6ac-179">**Охлаждение (в минутах):** 20</span><span class="sxs-lookup"><span data-stu-id="5f6ac-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="5f6ac-180">**Правило автоматического масштабирования (уменьшение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="5f6ac-181">**Правило автоматического масштабирования (уменьшение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="5f6ac-182">**Ресурс:** производство (среда службы приложений)</span><span class="sxs-lookup"><span data-stu-id="5f6ac-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="5f6ac-183">**Ресурс:** производство (среда службы приложений)</span><span class="sxs-lookup"><span data-stu-id="5f6ac-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="5f6ac-184">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="5f6ac-184">**Metric:** CPU %</span></span> |<span data-ttu-id="5f6ac-185">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="5f6ac-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="5f6ac-186">**Операции:** менее 30 %</span><span class="sxs-lookup"><span data-stu-id="5f6ac-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="5f6ac-187">**Операции:** менее 20 %</span><span class="sxs-lookup"><span data-stu-id="5f6ac-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="5f6ac-188">**Длительность:** 10 минут</span><span class="sxs-lookup"><span data-stu-id="5f6ac-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="5f6ac-189">**Длительность:** 15 минут</span><span class="sxs-lookup"><span data-stu-id="5f6ac-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="5f6ac-190">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="5f6ac-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="5f6ac-191">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="5f6ac-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="5f6ac-192">**Действие:** уменьшить количество на 1</span><span class="sxs-lookup"><span data-stu-id="5f6ac-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="5f6ac-193">**Действие:** уменьшить количество на 1</span><span class="sxs-lookup"><span data-stu-id="5f6ac-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="5f6ac-194">**Охлаждение (в минутах):** 20</span><span class="sxs-lookup"><span data-stu-id="5f6ac-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="5f6ac-195">**Охлаждение (в минутах):** 10</span><span class="sxs-lookup"><span data-stu-id="5f6ac-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="5f6ac-196">Скорость роста плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f6ac-196">App Service plan inflation rate</span></span>
<span data-ttu-id="5f6ac-197">Автоматически масштабирующиеся планы службы приложений масштабируются с определенной максимальной скоростью.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-197">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="5f6ac-198">Эту скорость можно рассчитать на основе значений, указанных в правиле автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-198">This rate can be calculated based on the values provided on the autoscale rule.</span></span>

<span data-ttu-id="5f6ac-199">Чтобы успешно применять автомасштабирование среды службы приложений, важно разбираться в значениях *скорости роста плана службы приложений* , а также уметь их рассчитывать, так как изменения масштаба рабочего пула вступают в силу не мгновенно.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-199">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span></span>

<span data-ttu-id="5f6ac-200">Скорость роста плана службы приложений рассчитывается так:</span><span class="sxs-lookup"><span data-stu-id="5f6ac-200">The App Service plan inflation rate is calculated as follows:</span></span>

![Расчет скорости роста плана службы приложений.][ASP-Inflation]

<span data-ttu-id="5f6ac-202">Для правила "Автоматическое масштабирование — увеличение масштаба" в профиле "Рабочие дни" производственного плана службы приложений расчет выглядит так:</span><span class="sxs-lookup"><span data-stu-id="5f6ac-202">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span></span>

![Скорость роста плана службы приложений для рабочих дней на основе правила "Автомасштабирование — увеличение масштаба".][Equation1]

<span data-ttu-id="5f6ac-204">Для правила "Автоматическое масштабирование — увеличение масштаба" в профиле "Выходные дни" производственного плана службы приложений эта формула выглядит так:</span><span class="sxs-lookup"><span data-stu-id="5f6ac-204">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>

![Скорость роста плана службы приложений для выходных дней на основе правила "Автомасштабирование — увеличение масштаба".][Equation2]

<span data-ttu-id="5f6ac-206">Это значение можно вычислить и для операций уменьшения масштаба.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="5f6ac-207">Для правила "Автоматическое масштабирование — уменьшение масштаба" в профиле "Рабочие дни" производственного плана службы приложений расчет выглядит так:</span><span class="sxs-lookup"><span data-stu-id="5f6ac-207">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span></span>

![Скорость роста плана службы приложений для рабочих дней на основе правила "Автомасштабирование — уменьшение масштаба".][Equation3]

<span data-ttu-id="5f6ac-209">Для правила "Автоматическое масштабирование — уменьшение масштаба" в профиле "Выходные дни" производственного плана службы приложений эта формула выглядит так:</span><span class="sxs-lookup"><span data-stu-id="5f6ac-209">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>  

![Скорость роста плана службы приложений для выходных дней на основе правила "Автомасштабирование — уменьшение масштаба".][Equation4]

<span data-ttu-id="5f6ac-211">Производственный план службы приложений может увеличиваться со скоростью восемь экземпляров в час в рабочие дни и четыре экземпляра в час в выходные дни.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-211">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span></span> <span data-ttu-id="5f6ac-212">Экземпляры могут высвобождаться с максимальной скоростью четыре экземпляра в час в рабочие дни и шесть экземпляров в час в выходные дни.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-212">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span></span>

<span data-ttu-id="5f6ac-213">Если в рабочем пуле размещено несколько планов службы приложений, вам нужно рассчитать *общую скорость роста* , то есть сумму скоростей роста для всех планов службы приложений, размещенных в этом рабочем пуле.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-213">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span></span>

![Расчет общей скорости роста по нескольким планам службы приложений, размещенным в рабочем пуле.][ASP-Total-Inflation]

### <a name="use-the-app-service-plan-inflation-rate-to-define-worker-pool-autoscale-rules"></a><span data-ttu-id="5f6ac-215">Использование показателей скорости роста плана службы приложений для определения правил автоматического масштабирования рабочего пула</span><span class="sxs-lookup"><span data-stu-id="5f6ac-215">Use the App Service plan inflation rate to define worker pool autoscale rules</span></span>
<span data-ttu-id="5f6ac-216">Для рабочих пулов, в которых размещены автоматически масштабирующиеся планы службы приложений, следует выделить резервную емкость (буфер).</span><span class="sxs-lookup"><span data-stu-id="5f6ac-216">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="5f6ac-217">Этот буфер нужен для автоматического увеличения или уменьшения плана службы приложений по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-217">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="5f6ac-218">Минимальный размер буфера рассчитывается с учетом общей скорости роста плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-218">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="5f6ac-219">Так как масштабирование среды службы приложений выполняется некоторое время, при любом изменении нужно учитывать дальнейшие колебания спроса, которые могут произойти в ходе операции.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-219">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="5f6ac-220">Чтобы включить в расчет эту задержку, мы рекомендуем использовать расчетную общую скорость роста плана службы приложений как минимальное число экземпляров, добавляемых для каждой операции автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-220">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="5f6ac-221">Эти сведения помогут Федору определить профиль и правила автоматического масштабирования:</span><span class="sxs-lookup"><span data-stu-id="5f6ac-221">With this information, Frank can define the following autoscale profile and rules:</span></span>

![Правила профиля автомасштабирования на примере бизнес-приложения.][Worker-Pool-Scale]

| <span data-ttu-id="5f6ac-223">**Профиль автоматического масштабирования — рабочие дни**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="5f6ac-224">**Профиль автоматического масштабирования — выходные дни**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="5f6ac-225">**Имя:** профиль рабочего дня</span><span class="sxs-lookup"><span data-stu-id="5f6ac-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="5f6ac-226">**Имя:** профиль выходного дня</span><span class="sxs-lookup"><span data-stu-id="5f6ac-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="5f6ac-227">**Масштабирование:** расписание и правила производительности</span><span class="sxs-lookup"><span data-stu-id="5f6ac-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="5f6ac-228">**Масштабирование:** расписание и правила производительности</span><span class="sxs-lookup"><span data-stu-id="5f6ac-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="5f6ac-229">**Профиль:** рабочие дни</span><span class="sxs-lookup"><span data-stu-id="5f6ac-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="5f6ac-230">**Профиль:** выходные дни</span><span class="sxs-lookup"><span data-stu-id="5f6ac-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="5f6ac-231">**Тип:** повторение</span><span class="sxs-lookup"><span data-stu-id="5f6ac-231">**Type:** Recurrence</span></span> |<span data-ttu-id="5f6ac-232">**Тип:** повторение</span><span class="sxs-lookup"><span data-stu-id="5f6ac-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="5f6ac-233">**Целевой диапазон:** 13–25 экземпляров</span><span class="sxs-lookup"><span data-stu-id="5f6ac-233">**Target range:** 13 to 25 instances</span></span> |<span data-ttu-id="5f6ac-234">**Целевой диапазон:** 6–15 экземпляров</span><span class="sxs-lookup"><span data-stu-id="5f6ac-234">**Target range:** 6 to 15 instances</span></span> |
| <span data-ttu-id="5f6ac-235">**Дни:** понедельник, вторник, среда, четверг, пятница</span><span class="sxs-lookup"><span data-stu-id="5f6ac-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="5f6ac-236">**Дни:** суббота, воскресенье</span><span class="sxs-lookup"><span data-stu-id="5f6ac-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="5f6ac-237">**Время начала:** 7:00</span><span class="sxs-lookup"><span data-stu-id="5f6ac-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="5f6ac-238">**Время начала:** 9:00</span><span class="sxs-lookup"><span data-stu-id="5f6ac-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="5f6ac-239">**Часовой пояс:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="5f6ac-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="5f6ac-240">**Часовой пояс:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="5f6ac-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="5f6ac-241">**Правило автоматического масштабирования (увеличение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="5f6ac-242">**Правило автоматического масштабирования (увеличение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="5f6ac-243">**Ресурс:** рабочий пул 1</span><span class="sxs-lookup"><span data-stu-id="5f6ac-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="5f6ac-244">**Ресурс:** рабочий пул 1</span><span class="sxs-lookup"><span data-stu-id="5f6ac-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="5f6ac-245">**Метрика:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="5f6ac-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="5f6ac-246">**Метрика:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="5f6ac-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="5f6ac-247">**Операции:** менее 8</span><span class="sxs-lookup"><span data-stu-id="5f6ac-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="5f6ac-248">**Операции:** менее 3</span><span class="sxs-lookup"><span data-stu-id="5f6ac-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="5f6ac-249">**Длительность:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="5f6ac-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="5f6ac-250">**Длительность:** 30 минут</span><span class="sxs-lookup"><span data-stu-id="5f6ac-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="5f6ac-251">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="5f6ac-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="5f6ac-252">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="5f6ac-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="5f6ac-253">**Действие:** увеличить количество на 8</span><span class="sxs-lookup"><span data-stu-id="5f6ac-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="5f6ac-254">**Действие:** увеличить количество на 3</span><span class="sxs-lookup"><span data-stu-id="5f6ac-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="5f6ac-255">**Охлаждение (в минутах):** 180</span><span class="sxs-lookup"><span data-stu-id="5f6ac-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="5f6ac-256">**Охлаждение (в минутах):** 180</span><span class="sxs-lookup"><span data-stu-id="5f6ac-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="5f6ac-257">**Правило автоматического масштабирования (уменьшение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="5f6ac-258">**Правило автоматического масштабирования (уменьшение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="5f6ac-259">**Ресурс:** рабочий пул 1</span><span class="sxs-lookup"><span data-stu-id="5f6ac-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="5f6ac-260">**Ресурс:** рабочий пул 1</span><span class="sxs-lookup"><span data-stu-id="5f6ac-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="5f6ac-261">**Метрика:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="5f6ac-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="5f6ac-262">**Метрика:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="5f6ac-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="5f6ac-263">**Операции:** более 8</span><span class="sxs-lookup"><span data-stu-id="5f6ac-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="5f6ac-264">**Операции:** более 3</span><span class="sxs-lookup"><span data-stu-id="5f6ac-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="5f6ac-265">**Длительность:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="5f6ac-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="5f6ac-266">**Длительность:** 15 минут</span><span class="sxs-lookup"><span data-stu-id="5f6ac-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="5f6ac-267">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="5f6ac-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="5f6ac-268">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="5f6ac-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="5f6ac-269">**Действие:** уменьшить количество на 2</span><span class="sxs-lookup"><span data-stu-id="5f6ac-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="5f6ac-270">**Действие:** уменьшить количество на 3</span><span class="sxs-lookup"><span data-stu-id="5f6ac-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="5f6ac-271">**Охлаждение (в минутах):** 120</span><span class="sxs-lookup"><span data-stu-id="5f6ac-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="5f6ac-272">**Охлаждение (в минутах):** 120</span><span class="sxs-lookup"><span data-stu-id="5f6ac-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="5f6ac-273">Целевой диапазон, определяемый в профиле, вычисляется по минимальному числу экземпляров, указанных в профиле для плана службы приложений с учетом емкости буфера.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-273">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span></span>

<span data-ttu-id="5f6ac-274">Максимальный диапазон вычисляется как сумма всех максимальных диапазонов для всех планов службы приложений, размещенных в рабочем пуле.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-274">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span></span>

<span data-ttu-id="5f6ac-275">Значение увеличения для правил увеличения масштаба должно включать не менее одной скорости роста плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-275">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="5f6ac-276">Значение уменьшения можно установить в пределах от половины до одной скорости роста плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-276">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="5f6ac-277">Автоматическое масштабирование для интерфейсного пула</span><span class="sxs-lookup"><span data-stu-id="5f6ac-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="5f6ac-278">Правила автомасштабирования для интерфейсных пулов проще, чем правила для рабочих пулов.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="5f6ac-279">Важно,</span><span class="sxs-lookup"><span data-stu-id="5f6ac-279">Primarily, you should</span></span>  
<span data-ttu-id="5f6ac-280">чтобы при определении продолжительности измерений и таймеров ожидания вы учитывали, что масштабирование плана службы приложений не происходит мгновенно.</span><span class="sxs-lookup"><span data-stu-id="5f6ac-280">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="5f6ac-281">Федор знает, что частота ошибок увеличивается после достижения внешним интерфейсом 80 % загрузки ЦП. Он устанавливает правило автомасштабирования для увеличения экземпляров следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5f6ac-281">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span></span>

![Параметры автомасштабирования для интерфейсного пула.][Front-End-Scale]

| <span data-ttu-id="5f6ac-283">**Профиль автоматического масштабирования — внешние интерфейсы**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="5f6ac-284">**Имя:** автоматическое масштабирование — внешние интерфейсы</span><span class="sxs-lookup"><span data-stu-id="5f6ac-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="5f6ac-285">**Масштабирование:** расписание и правила производительности</span><span class="sxs-lookup"><span data-stu-id="5f6ac-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="5f6ac-286">**Профиль:** ежедневно</span><span class="sxs-lookup"><span data-stu-id="5f6ac-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="5f6ac-287">**Тип:** повторение</span><span class="sxs-lookup"><span data-stu-id="5f6ac-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="5f6ac-288">**Целевой диапазон:** 3–10 экземпляров</span><span class="sxs-lookup"><span data-stu-id="5f6ac-288">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="5f6ac-289">**Дни:** ежедневно</span><span class="sxs-lookup"><span data-stu-id="5f6ac-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="5f6ac-290">**Время начала:** 9:00</span><span class="sxs-lookup"><span data-stu-id="5f6ac-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="5f6ac-291">**Часовой пояс:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="5f6ac-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="5f6ac-292">**Правило автоматического масштабирования (увеличение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="5f6ac-293">**Ресурс:** пул внешних интерфейсов</span><span class="sxs-lookup"><span data-stu-id="5f6ac-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="5f6ac-294">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="5f6ac-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="5f6ac-295">**Операции:** более 60 %</span><span class="sxs-lookup"><span data-stu-id="5f6ac-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="5f6ac-296">**Длительность:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="5f6ac-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="5f6ac-297">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="5f6ac-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="5f6ac-298">**Действие:** увеличить количество на 3</span><span class="sxs-lookup"><span data-stu-id="5f6ac-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="5f6ac-299">**Охлаждение (в минутах):** 120</span><span class="sxs-lookup"><span data-stu-id="5f6ac-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="5f6ac-300">**Правило автоматического масштабирования (уменьшение масштаба)**</span><span class="sxs-lookup"><span data-stu-id="5f6ac-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="5f6ac-301">**Ресурс:** рабочий пул 1</span><span class="sxs-lookup"><span data-stu-id="5f6ac-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="5f6ac-302">**Метрика:** % ЦП</span><span class="sxs-lookup"><span data-stu-id="5f6ac-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="5f6ac-303">**Операции:** менее 30 %</span><span class="sxs-lookup"><span data-stu-id="5f6ac-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="5f6ac-304">**Длительность:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="5f6ac-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="5f6ac-305">**Агрегация по времени:** среднее</span><span class="sxs-lookup"><span data-stu-id="5f6ac-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="5f6ac-306">**Действие:** уменьшить количество на 3</span><span class="sxs-lookup"><span data-stu-id="5f6ac-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="5f6ac-307">**Охлаждение (в минутах):** 120</span><span class="sxs-lookup"><span data-stu-id="5f6ac-307">**Cool down (minutes):** 120</span></span> |

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
