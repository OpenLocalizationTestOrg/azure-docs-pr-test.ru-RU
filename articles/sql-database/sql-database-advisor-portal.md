---
title: "рекомендации по повышению производительности aaaApply - базы данных SQL Azure | Документы Microsoft"
description: "Рекомендации по повышению производительности Azure портала toofind hello, оптимизировать производительность базы данных SQL Azure или toocorrect можно использовать некоторые проблемы, обнаруженной в рабочей нагрузке."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="22fa7-103">Поиск и применение рекомендаций по производительности</span><span class="sxs-lookup"><span data-stu-id="22fa7-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="22fa7-104">Рекомендации по повышению производительности Azure портала toofind hello, оптимизировать производительность базы данных SQL Azure или toocorrect можно использовать некоторые проблемы, обнаруженной в рабочей нагрузке.</span><span class="sxs-lookup"><span data-stu-id="22fa7-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="22fa7-105">**Рекомендации по производительности** странице на портале Azure можно toofind hello top рекомендаций, основанных на потенциальные последствия.</span><span class="sxs-lookup"><span data-stu-id="22fa7-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="22fa7-106">Просмотр рекомендаций</span><span class="sxs-lookup"><span data-stu-id="22fa7-106">Viewing recommendations</span></span>

<span data-ttu-id="22fa7-107">tooview и применить рекомендации по повышению производительности, требуется hello правильный [управления доступом на основе ролей](../active-directory/role-based-access-control-what-is.md) разрешения в Azure.</span><span class="sxs-lookup"><span data-stu-id="22fa7-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="22fa7-108">**Модуль чтения**, **участника базы данных SQL** разрешения, необходимые tooview рекомендации, и **владельца**, **участника базы данных SQL** требуются разрешения tooexecute каких-либо действий; Создание или удаление индексов и создание индекса.</span><span class="sxs-lookup"><span data-stu-id="22fa7-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="22fa7-109">Используйте следующие рекомендации по повышению производительности toofind действия на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="22fa7-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="22fa7-110">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="22fa7-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="22fa7-111">Go слишком**дополнительные службы** > **баз данных SQL**и выберите вашу базу данных.</span><span class="sxs-lookup"><span data-stu-id="22fa7-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="22fa7-112">Перейдите в слишком**рекомендации по производительности** tooview доступные рекомендации для hello выбранной базы данных.</span><span class="sxs-lookup"><span data-stu-id="22fa7-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="22fa7-113">Рекомендации по повышению производительности принадлежат shonw аналогичные toohello таблицы hello, показанной на следующий рисунок hello.</span><span class="sxs-lookup"><span data-stu-id="22fa7-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![Рекомендации](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="22fa7-115">Рекомендации сортируются по их потенциальное воздействие на производительность в hello следующие категории:</span><span class="sxs-lookup"><span data-stu-id="22fa7-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="22fa7-116">Влияние</span><span class="sxs-lookup"><span data-stu-id="22fa7-116">Impact</span></span> | <span data-ttu-id="22fa7-117">Описание</span><span class="sxs-lookup"><span data-stu-id="22fa7-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22fa7-118">Высокий</span><span class="sxs-lookup"><span data-stu-id="22fa7-118">High</span></span> |<span data-ttu-id="22fa7-119">Высокая степень влияния на рекомендации должен предоставить hello наибольшее влияние на производительность.</span><span class="sxs-lookup"><span data-stu-id="22fa7-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="22fa7-120">Средний</span><span class="sxs-lookup"><span data-stu-id="22fa7-120">Medium</span></span> |<span data-ttu-id="22fa7-121">Рекомендации со средним уровнем влияния должны улучшить производительность, но не существенным образом.</span><span class="sxs-lookup"><span data-stu-id="22fa7-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="22fa7-122">Низкий</span><span class="sxs-lookup"><span data-stu-id="22fa7-122">Low</span></span> |<span data-ttu-id="22fa7-123">Рекомендации с низким уровнем влияния должны улучшить производительность, но улучшения не будут значительными.</span><span class="sxs-lookup"><span data-stu-id="22fa7-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="22fa7-124">База данных SQL Azure должен toomonitor действий по крайней мере за день в порядке tooidentify некоторые рекомендации.</span><span class="sxs-lookup"><span data-stu-id="22fa7-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="22fa7-125">Hello базы данных SQL Azure легко можно оптимизировать для шаблонов согласованный запрос чем для произвольного неравномерного всплески активности.</span><span class="sxs-lookup"><span data-stu-id="22fa7-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="22fa7-126">Здравствуйте, рекомендации, если они не доступны corrently **рекомендация производительности** отображается сообщение о том, почему это происходит.</span><span class="sxs-lookup"><span data-stu-id="22fa7-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="22fa7-127">Можно также просмотреть состояние hello hello журнала операций.</span><span class="sxs-lookup"><span data-stu-id="22fa7-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="22fa7-128">Выберите состояние или рекомендация toosee Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="22fa7-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="22fa7-129">Ниже приведен пример «Создание индекса» рекомендации по hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="22fa7-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![Создание индекса](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="22fa7-131">Применение рекомендаций</span><span class="sxs-lookup"><span data-stu-id="22fa7-131">Applying recommendations</span></span>
<span data-ttu-id="22fa7-132">База данных SQL Azure предоставляет полный контроль над как рекомендации могут включить с помощью любого из следующих трех вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="22fa7-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="22fa7-133">применять отдельные рекомендаций по одной;</span><span class="sxs-lookup"><span data-stu-id="22fa7-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="22fa7-134">Включить hello автоматической настройки tooautomatically применить рекомендации.</span><span class="sxs-lookup"><span data-stu-id="22fa7-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="22fa7-135">tooimplement рекомендации вручную, выполните hello, рекомендуется использовать скрипт T-SQL к базе данных.</span><span class="sxs-lookup"><span data-stu-id="22fa7-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="22fa7-136">Выберите любой tooview рекомендация его данные и нажмите кнопку **просмотреть скрипт** tooreview hello точные сведения об способ создания рекомендаций hello.</span><span class="sxs-lookup"><span data-stu-id="22fa7-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="22fa7-137">Hello находится в оперативном режиме во время применения рекомендаций hello — с помощью рекомендации по производительности или автоматической настройки никогда не переводит базу данных в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="22fa7-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="22fa7-138">Применение отдельной рекомендации</span><span class="sxs-lookup"><span data-stu-id="22fa7-138">Apply an individual recommendation</span></span>
<span data-ttu-id="22fa7-139">Рекомендации можно просматривать и применять по одной.</span><span class="sxs-lookup"><span data-stu-id="22fa7-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="22fa7-140">На hello **рекомендации** колонке выберите рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="22fa7-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="22fa7-141">На hello **сведения** колонки щелкните **применить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="22fa7-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![Применить рекомендацию](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="22fa7-143">Выбранные рекомендации применяются hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="22fa7-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="22fa7-144">Удаление из списка hello рекомендации</span><span class="sxs-lookup"><span data-stu-id="22fa7-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="22fa7-145">Если список рекомендаций, содержит элементы, которые должны tooremove из списка hello, вы можете отменить hello рекомендации:</span><span class="sxs-lookup"><span data-stu-id="22fa7-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="22fa7-146">Выберите в списке hello рекомендации **рекомендации** tooopen hello сведения.</span><span class="sxs-lookup"><span data-stu-id="22fa7-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="22fa7-147">Нажмите кнопку **отменить** на hello **сведения** колонку.</span><span class="sxs-lookup"><span data-stu-id="22fa7-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="22fa7-148">При необходимости можно добавлять, отвергнутые элементы обратно toohello **рекомендации** списка:</span><span class="sxs-lookup"><span data-stu-id="22fa7-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="22fa7-149">На hello **рекомендации** колонки щелкните **удаляется представление**.</span><span class="sxs-lookup"><span data-stu-id="22fa7-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="22fa7-150">Выберите отмененный элемент из списка tooview hello сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="22fa7-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="22fa7-151">При необходимости щелкните **отменить отменить** tooadd hello индекс задней toohello основной список **рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="22fa7-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="22fa7-152">Включение автоматической настройки</span><span class="sxs-lookup"><span data-stu-id="22fa7-152">Enable automatic tuning</span></span>
<span data-ttu-id="22fa7-153">Рекомендации tooimplement hello базы данных SQL Azure можно установить автоматически.</span><span class="sxs-lookup"><span data-stu-id="22fa7-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="22fa7-154">В этом случае появляющиеся рекомендации будут применяться автоматически.</span><span class="sxs-lookup"><span data-stu-id="22fa7-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="22fa7-155">Как все рекомендации, которые управляются hello службы hello влияние на производительность в случае отрицательного hello рекомендации будут отменены.</span><span class="sxs-lookup"><span data-stu-id="22fa7-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="22fa7-156">На hello **рекомендации** колонка, щелкните **автоматизация**:</span><span class="sxs-lookup"><span data-stu-id="22fa7-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![Настройки помощника](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="22fa7-158">Выберите tooautomate действия:</span><span class="sxs-lookup"><span data-stu-id="22fa7-158">Select actions tooautomate:</span></span>
   
    ![Рекомендованные индексы](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="22fa7-160">Вручную запустить hello, рекомендуется использовать скрипт T-SQL</span><span class="sxs-lookup"><span data-stu-id="22fa7-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="22fa7-161">Выберите рекомендацию и щелкните **Показать скрипт**.</span><span class="sxs-lookup"><span data-stu-id="22fa7-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="22fa7-162">Запустите этот сценарий для базы данных toomanually применить рекомендации hello.</span><span class="sxs-lookup"><span data-stu-id="22fa7-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="22fa7-163">*Индексы, которые выполняются вручную не отслеживаются и проверяется производительность службой hello* , рекомендуется отслеживать эти индексы, после создания tooverify они обеспечивают повышение производительности и настройки или удалить их, если обязательно.</span><span class="sxs-lookup"><span data-stu-id="22fa7-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="22fa7-164">Дополнительные сведения о создании индексов см. в статье [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="22fa7-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="22fa7-165">Отмена рекомендаций</span><span class="sxs-lookup"><span data-stu-id="22fa7-165">Canceling recommendations</span></span>
<span data-ttu-id="22fa7-166">Рекомендации с состоянием **Ожидание**, **Проверка** или **Успешно** можно отменить.</span><span class="sxs-lookup"><span data-stu-id="22fa7-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="22fa7-167">Рекомендация с состоянием **Выполняется** не может быть отменена.</span><span class="sxs-lookup"><span data-stu-id="22fa7-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="22fa7-168">Выберите рекомендации в hello **настройки журнала** область tooopen hello **рекомендациями** колонку.</span><span class="sxs-lookup"><span data-stu-id="22fa7-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="22fa7-169">Нажмите кнопку **отменить** tooabort hello процесс применения рекомендаций hello.</span><span class="sxs-lookup"><span data-stu-id="22fa7-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="22fa7-170">Мониторинг операций</span><span class="sxs-lookup"><span data-stu-id="22fa7-170">Monitoring operations</span></span>
<span data-ttu-id="22fa7-171">Применение рекомендаций может происходить не мгновенно.</span><span class="sxs-lookup"><span data-stu-id="22fa7-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="22fa7-172">Hello портал предоставляет сведения о состоянии hello рекомендации.</span><span class="sxs-lookup"><span data-stu-id="22fa7-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="22fa7-173">Hello представлены возможные состояния, которые могут быть индекса в:</span><span class="sxs-lookup"><span data-stu-id="22fa7-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="22fa7-174">Состояние</span><span class="sxs-lookup"><span data-stu-id="22fa7-174">Status</span></span> | <span data-ttu-id="22fa7-175">Описание</span><span class="sxs-lookup"><span data-stu-id="22fa7-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22fa7-176">Ожидает</span><span class="sxs-lookup"><span data-stu-id="22fa7-176">Pending</span></span> |<span data-ttu-id="22fa7-177">Команда на применение рекомендации получена и запланирована для выполнения.</span><span class="sxs-lookup"><span data-stu-id="22fa7-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="22fa7-178">Выполняется</span><span class="sxs-lookup"><span data-stu-id="22fa7-178">Executing</span></span> |<span data-ttu-id="22fa7-179">Происходит применение рекомендаций Hello.</span><span class="sxs-lookup"><span data-stu-id="22fa7-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="22fa7-180">Проверка</span><span class="sxs-lookup"><span data-stu-id="22fa7-180">Verifying</span></span> |<span data-ttu-id="22fa7-181">Выполнено успешное применение рекомендаций и hello службы он измеряет преимущества hello.</span><span class="sxs-lookup"><span data-stu-id="22fa7-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="22fa7-182">Успешно</span><span class="sxs-lookup"><span data-stu-id="22fa7-182">Success</span></span> |<span data-ttu-id="22fa7-183">Рекомендация успешно применена, и преимущества были оценены.</span><span class="sxs-lookup"><span data-stu-id="22fa7-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="22fa7-184">Ошибка</span><span class="sxs-lookup"><span data-stu-id="22fa7-184">Error</span></span> |<span data-ttu-id="22fa7-185">Произошла ошибка во время процесса hello применения рекомендаций hello.</span><span class="sxs-lookup"><span data-stu-id="22fa7-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="22fa7-186">Это может быть временная проблема или таблицу toohello изменений схемы и скрипт hello больше не действительна.</span><span class="sxs-lookup"><span data-stu-id="22fa7-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="22fa7-187">Возврат</span><span class="sxs-lookup"><span data-stu-id="22fa7-187">Reverting</span></span> |<span data-ttu-id="22fa7-188">Рекомендация Hello была применена, но определен как не высокопроизводительных и автоматически выполняется откат.</span><span class="sxs-lookup"><span data-stu-id="22fa7-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="22fa7-189">Отмена</span><span class="sxs-lookup"><span data-stu-id="22fa7-189">Reverted</span></span> |<span data-ttu-id="22fa7-190">Рекомендация Hello была отменена.</span><span class="sxs-lookup"><span data-stu-id="22fa7-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="22fa7-191">Щелкните рекомендацию в процессе из списка toosee hello Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="22fa7-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![Рекомендованные индексы](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="22fa7-193">Отмена рекомендации</span><span class="sxs-lookup"><span data-stu-id="22fa7-193">Reverting a recommendation</span></span>
<span data-ttu-id="22fa7-194">Если вы использовали hello производительности рекомендации tooapply hello рекомендации (то есть вы вручную не запускали скрипт hello T-SQL) он автоматически вернется его при обнаружении hello производительности влияние toobe отрицательное.</span><span class="sxs-lookup"><span data-stu-id="22fa7-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="22fa7-195">Если для какой-либо причине, то необходимо просто toorevert рекомендации можно сделать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="22fa7-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="22fa7-196">Выберите успешно применено рекомендации в hello **настройки журнала** области.</span><span class="sxs-lookup"><span data-stu-id="22fa7-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="22fa7-197">Нажмите кнопку **Revert** на hello **рекомендацией** колонку.</span><span class="sxs-lookup"><span data-stu-id="22fa7-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![Рекомендованные индексы](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="22fa7-199">Мониторинг влияния рекомендаций по индексам на производительность</span><span class="sxs-lookup"><span data-stu-id="22fa7-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="22fa7-200">После успешного рекомендаций (в настоящее время операции с индексами и параметризовать запросы рекомендации только) можно щелкнуть **подробных сведений о запросов** на tooopen колонки сведений рекомендация hello [запроса Подробные сведения о производительности](sql-database-query-performance.md) и увидеть влияние на производительность hello нерегламентированными запросы.</span><span class="sxs-lookup"><span data-stu-id="22fa7-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![Мониторинг влияния на производительность](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="22fa7-202">Сводка</span><span class="sxs-lookup"><span data-stu-id="22fa7-202">Summary</span></span>
<span data-ttu-id="22fa7-203">База данных SQL Azure предоставляет рекомендации по производительности базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="22fa7-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="22fa7-204">Благодаря сценариям T-SQL, а также возможностям индивидуального или полностью автоматизированного управления вы получаете помощь в оптимизации базы данных и, таким образом, можете значительно повысить производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="22fa7-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22fa7-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22fa7-205">Next steps</span></span>
<span data-ttu-id="22fa7-206">Отслеживание рекомендаций и продолжить tooapply их toorefine производительности.</span><span class="sxs-lookup"><span data-stu-id="22fa7-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="22fa7-207">Рабочие нагрузки базы данных являются динамическими и меняются непрерывно.</span><span class="sxs-lookup"><span data-stu-id="22fa7-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="22fa7-208">База данных SQL Azure будут продолжать toomonitor и предоставить рекомендации, которые потенциально могут увеличить производительность вашей базы данных.</span><span class="sxs-lookup"><span data-stu-id="22fa7-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="22fa7-209">В разделе [автоматической настройки](sql-database-automatic-tuning.md) hello toolearn Дополнительные сведения об автоматической настройки в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="22fa7-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="22fa7-210">Общие сведения о рекомендациях по производительности базы данных SQL Azure см. в статье [Помощник по работе с базами данных SQL](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="22fa7-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="22fa7-211">В разделе [подробных сведений о производительности запросов](sql-database-query-performance.md) toolearn о просмотре hello влияние на производительность запросов top.</span><span class="sxs-lookup"><span data-stu-id="22fa7-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="22fa7-212">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="22fa7-212">Additional resources</span></span>
* [<span data-ttu-id="22fa7-213">Хранилище запросов</span><span class="sxs-lookup"><span data-stu-id="22fa7-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="22fa7-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="22fa7-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="22fa7-215">Контроль доступа на основе ролей</span><span class="sxs-lookup"><span data-stu-id="22fa7-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

