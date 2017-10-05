---
title: "Диагностика сбоев в Azure Logic Apps | Документация Майкрософт"
description: "Описание распространенных способов анализа сбоев приложений логики"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 814e6f93088cdd96b0a663d2a7494b5a11470d99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="4c71c-103">Диагностика сбоев приложений логики</span><span class="sxs-lookup"><span data-stu-id="4c71c-103">Diagnose logic app failures</span></span>
<span data-ttu-id="4c71c-104">Когда вы сталкиваетесь с проблемами или сбоями в работе приложений логики, для поиска их причин можно применять разные подходы.</span><span class="sxs-lookup"><span data-stu-id="4c71c-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="4c71c-105">Инструменты портала Azure</span><span class="sxs-lookup"><span data-stu-id="4c71c-105">Azure portal tools</span></span>
<span data-ttu-id="4c71c-106">Портал Azure предоставляет множество инструментов для диагностики каждого приложения логики на любом этапе.</span><span class="sxs-lookup"><span data-stu-id="4c71c-106">The Azure portal provides many tools to diagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="4c71c-107">Журнал триггера</span><span class="sxs-lookup"><span data-stu-id="4c71c-107">Trigger history</span></span>

<span data-ttu-id="4c71c-108">Каждое приложение логики имеет по крайней мере один триггер.</span><span class="sxs-lookup"><span data-stu-id="4c71c-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="4c71c-109">Если вы заметите, что определенные приложения не запускаются, первым делом следует проверить журнал триггеров.</span><span class="sxs-lookup"><span data-stu-id="4c71c-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span></span> <span data-ttu-id="4c71c-110">Журнал триггеров можно открыть в главной колонке приложений логики.</span><span class="sxs-lookup"><span data-stu-id="4c71c-110">You can access the trigger history on the logic app'ss main blade.</span></span>

![Поиск журнала триггера][1]

<span data-ttu-id="4c71c-112">В журнале триггеров отображается список всех попыток приложения логики с использованием триггера.</span><span class="sxs-lookup"><span data-stu-id="4c71c-112">The trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="4c71c-113">Вы можете щелкнуть любую из записей, чтобы получить подробные сведения, например входные и выходные данные, которые были созданы при попытке запуска по триггеру.</span><span class="sxs-lookup"><span data-stu-id="4c71c-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span></span> <span data-ttu-id="4c71c-114">Если вы видите сбой триггера, выберите такой триггер и щелкните ссылку **Выходные данные**, чтобы просмотреть все созданные сообщения об ошибках, например сообщение о неправильных учетных данных для FTP-подключения.</span><span class="sxs-lookup"><span data-stu-id="4c71c-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="4c71c-115">Ниже приводятся разные возможные статусы.</span><span class="sxs-lookup"><span data-stu-id="4c71c-115">The different statuses you might see are:</span></span>

* <span data-ttu-id="4c71c-116">**Пропущено**.</span><span class="sxs-lookup"><span data-stu-id="4c71c-116">**Skipped**.</span></span> <span data-ttu-id="4c71c-117">Триггер опросил конечную точку на предмет наличия данных и получил в ответ сообщение о том, что доступных данных нет.</span><span class="sxs-lookup"><span data-stu-id="4c71c-117">The endpoint was polled to check for data and received a response that no data was available.</span></span>
* <span data-ttu-id="4c71c-118">**Успешно**.</span><span class="sxs-lookup"><span data-stu-id="4c71c-118">**Succeeded**.</span></span> <span data-ttu-id="4c71c-119">Триггер получил ответ, что данные доступны.</span><span class="sxs-lookup"><span data-stu-id="4c71c-119">The trigger received a response that data was available.</span></span> <span data-ttu-id="4c71c-120">Это состояние может быть вызвано запускаемым вручную триггером, а также повторяющим или опрашиваемым триггером.</span><span class="sxs-lookup"><span data-stu-id="4c71c-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="4c71c-121">Обычно такое состояние сопровождается статусом **Fired** (Запущено). Но это может быть не так, если в представлении кода вы указали условие или команду SplitOn, которая не была выполнена.</span><span class="sxs-lookup"><span data-stu-id="4c71c-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="4c71c-122">**Сбой**.</span><span class="sxs-lookup"><span data-stu-id="4c71c-122">**Failed**.</span></span> <span data-ttu-id="4c71c-123">Произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="4c71c-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="4c71c-124">Запуск триггера вручную</span><span class="sxs-lookup"><span data-stu-id="4c71c-124">Start a trigger manually</span></span>

<span data-ttu-id="4c71c-125">Если вы хотите, чтобы приложение логики немедленно проверило доступность триггера, не дожидаясь следующего повторения, можно запустить проверку принудительно, щелкнув ссылку **Выбрать триггер** в главной колонке.</span><span class="sxs-lookup"><span data-stu-id="4c71c-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span></span> <span data-ttu-id="4c71c-126">Например, если щелкнуть эту ссылку для триггера Dropbox, рабочий процесс немедленно обратится к Dropbox и проверит наличие новых файлов.</span><span class="sxs-lookup"><span data-stu-id="4c71c-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="4c71c-127">Журнал выполнения</span><span class="sxs-lookup"><span data-stu-id="4c71c-127">Run history</span></span>

<span data-ttu-id="4c71c-128">Каждое срабатывание триггера завершается запуском.</span><span class="sxs-lookup"><span data-stu-id="4c71c-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="4c71c-129">Состояние запуска можно просмотреть в главной колонке, содержащей большой объем сведений, которые позволяют разобраться в событиях, произошедших при выполнении рабочего потока.</span><span class="sxs-lookup"><span data-stu-id="4c71c-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span></span>

![Поиск журнала выполнения][2]

<span data-ttu-id="4c71c-131">Отображается одно из следующих состояний запуска:</span><span class="sxs-lookup"><span data-stu-id="4c71c-131">A run displays one of the following statuses:</span></span>

* <span data-ttu-id="4c71c-132">**Успешно**.</span><span class="sxs-lookup"><span data-stu-id="4c71c-132">**Succeeded**.</span></span> <span data-ttu-id="4c71c-133">Все действия выполнены успешно.</span><span class="sxs-lookup"><span data-stu-id="4c71c-133">All actions succeeded.</span></span> <span data-ttu-id="4c71c-134">Если происходили сбои, то они были успешно обработаны другими действиями в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="4c71c-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span></span> <span data-ttu-id="4c71c-135">Например, было запущено новое действие после действия, завершившегося сбоем.</span><span class="sxs-lookup"><span data-stu-id="4c71c-135">That is, the failure was handled by an action that was set to run after a failed action.</span></span>
* <span data-ttu-id="4c71c-136">**Сбой**.</span><span class="sxs-lookup"><span data-stu-id="4c71c-136">**Failed**.</span></span> <span data-ttu-id="4c71c-137">По крайней мере одно действие завершилось ошибкой, которая не была обработана последующими действиями в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="4c71c-137">At least one action had a failure that was not handled by an action later in the workflow.</span></span>
* <span data-ttu-id="4c71c-138">**Отменено**.</span><span class="sxs-lookup"><span data-stu-id="4c71c-138">**Cancelled**.</span></span> <span data-ttu-id="4c71c-139">Рабочий процесс был запущен, но получил запрос на отмену.</span><span class="sxs-lookup"><span data-stu-id="4c71c-139">The workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="4c71c-140">**Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="4c71c-140">**Running**.</span></span> <span data-ttu-id="4c71c-141">Рабочий процесс выполняется в данный момент.</span><span class="sxs-lookup"><span data-stu-id="4c71c-141">The workflow is currently running.</span></span> <span data-ttu-id="4c71c-142">Это состояние может возникнуть в регулируемых рабочих процессах или в рамках текущего тарифного плана.</span><span class="sxs-lookup"><span data-stu-id="4c71c-142">This status might occur for throttled workflows, or because of the current pricing plan.</span></span> <span data-ttu-id="4c71c-143">Ограничения для действий описаны на [странице цен](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="4c71c-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="4c71c-144">Настройка диагностики (диаграммы под журналом выполнения) также поможет узнать, происходят ли события регулирования.</span><span class="sxs-lookup"><span data-stu-id="4c71c-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="4c71c-145">Просматривая журнал выполнения, можно ознакомиться с подробностями процесса.</span><span class="sxs-lookup"><span data-stu-id="4c71c-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="4c71c-146">Выходные данные триггера</span><span class="sxs-lookup"><span data-stu-id="4c71c-146">Trigger outputs</span></span>

<span data-ttu-id="4c71c-147">В выходных данных триггера отображаются данные, которые поступают от триггера.</span><span class="sxs-lookup"><span data-stu-id="4c71c-147">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="4c71c-148">Они помогут разобраться, все ли свойства возвращаются так, как требуется.</span><span class="sxs-lookup"><span data-stu-id="4c71c-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="4c71c-149">Если вы не понимаете некоторое содержимое, узнайте, как Azure Logic Apps [обрабатывает разные типы содержимого](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="4c71c-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Примеры выводных данных триггера][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="4c71c-151">Входные и выходные данные действия</span><span class="sxs-lookup"><span data-stu-id="4c71c-151">Action inputs and outputs</span></span>

<span data-ttu-id="4c71c-152">Вы можете более подробно изучить входные и выходные данные, которые получало и возвращало действие.</span><span class="sxs-lookup"><span data-stu-id="4c71c-152">You can drill into the inputs and outputs that an action received.</span></span> <span data-ttu-id="4c71c-153">Эти сведения помогут понять, какие данные и в каком количестве были переданы, а также найти любые созданные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="4c71c-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span></span>

![Входные и выходные данные действия][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="4c71c-155">Среда отладки рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="4c71c-155">Debug workflow runtime</span></span>

<span data-ttu-id="4c71c-156">Наряду с отслеживанием входящих и выходящих данных и триггеров запуска, можно добавить в рабочий процесс дополнительные действия для отладки.</span><span class="sxs-lookup"><span data-stu-id="4c71c-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span></span> 
<span data-ttu-id="4c71c-157">Например, вы можете включить в рабочий процесс такой мощный инструмент, как [RequestBin](http://requestb.in).</span><span class="sxs-lookup"><span data-stu-id="4c71c-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="4c71c-158">RequestBin позволяет настроить инспектор HTTP-запроса, чтобы точно выяснить размер, форму и формат HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="4c71c-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="4c71c-159">Вы можете создать элемент RequestBin и вставить в действие HTTP POST своего приложения логики URL-адрес с содержимым тела запроса, которое необходимо протестировать (например, выражением, выходными данными другого шага и т. д.).</span><span class="sxs-lookup"><span data-stu-id="4c71c-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span></span> <span data-ttu-id="4c71c-160">После выполнения приложения логики следует обновить этот элемент RequestBin, чтобы увидеть, как механизм приложений логики создавал запрос.</span><span class="sxs-lookup"><span data-stu-id="4c71c-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
