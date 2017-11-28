---
title: "ошибки aaaDiagnose - приложения логики Azure | Документы Microsoft"
description: "Общие способы toounderstand, где произошел сбой приложения логики"
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
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="4914b-103">Диагностика сбоев приложений логики</span><span class="sxs-lookup"><span data-stu-id="4914b-103">Diagnose logic app failures</span></span>
<span data-ttu-id="4914b-104">При возникновении ошибки или сбои вместе со своими приложениями логики, существует несколько подходов, чтобы лучше понять, откуда поступают hello сбоев.</span><span class="sxs-lookup"><span data-stu-id="4914b-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where hello failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="4914b-105">Инструменты портала Azure</span><span class="sxs-lookup"><span data-stu-id="4914b-105">Azure portal tools</span></span>
<span data-ttu-id="4914b-106">Hello портал Azure предоставляет множество средств toodiagnose каждого логики приложения на каждом шаге.</span><span class="sxs-lookup"><span data-stu-id="4914b-106">hello Azure portal provides many tools toodiagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="4914b-107">Журнал триггера</span><span class="sxs-lookup"><span data-stu-id="4914b-107">Trigger history</span></span>

<span data-ttu-id="4914b-108">Каждое приложение логики имеет по крайней мере один триггер.</span><span class="sxs-lookup"><span data-stu-id="4914b-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="4914b-109">Если вы заметили, что не запуск приложений, найдите первый журнал hello триггера для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="4914b-109">If you notice that apps aren't firing, look first at hello trigger history for more information.</span></span> <span data-ttu-id="4914b-110">Можно открыть журнал триггер hello hello логику app'ss главной колонке.</span><span class="sxs-lookup"><span data-stu-id="4914b-110">You can access hello trigger history on hello logic app'ss main blade.</span></span>

![Поиск журнала триггер hello][1]

<span data-ttu-id="4914b-112">Журнал триггер Hello перечислены все попытки триггер, внесенных в приложение логику.</span><span class="sxs-lookup"><span data-stu-id="4914b-112">hello trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="4914b-113">Можно щелкнуть каждый toodrill попытка триггера в детали hello специально, все входные данные или созданные выходные данные, которые hello попытка триггера.</span><span class="sxs-lookup"><span data-stu-id="4914b-113">You can click each trigger attempt toodrill into hello details, specifically, any inputs or outputs that hello trigger attempt generated.</span></span> <span data-ttu-id="4914b-114">Если вы найдете неудачных триггеры, щелкните попытки hello триггер и выберите hello **выходов** связать tooreview созданного сообщения об ошибках, например, для FTP учетные данные, которые не являются допустимыми.</span><span class="sxs-lookup"><span data-stu-id="4914b-114">If you find failed triggers, select hello trigger attempt and choose hello **Outputs** link tooreview any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="4914b-115">Hello различные состояния, которые можно увидеть являются:</span><span class="sxs-lookup"><span data-stu-id="4914b-115">hello different statuses you might see are:</span></span>

* <span data-ttu-id="4914b-116">**Пропущено**.</span><span class="sxs-lookup"><span data-stu-id="4914b-116">**Skipped**.</span></span> <span data-ttu-id="4914b-117">Конечная точка Hello был запрошенными toocheck для данных и получен ответ, что данные не были доступны.</span><span class="sxs-lookup"><span data-stu-id="4914b-117">hello endpoint was polled toocheck for data and received a response that no data was available.</span></span>
* <span data-ttu-id="4914b-118">**Успешно**.</span><span class="sxs-lookup"><span data-stu-id="4914b-118">**Succeeded**.</span></span> <span data-ttu-id="4914b-119">триггер Hello получил ответное сообщение о том, что данные были доступными.</span><span class="sxs-lookup"><span data-stu-id="4914b-119">hello trigger received a response that data was available.</span></span> <span data-ttu-id="4914b-120">Это состояние может быть вызвано запускаемым вручную триггером, а также повторяющим или опрашиваемым триггером.</span><span class="sxs-lookup"><span data-stu-id="4914b-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="4914b-121">Это состояние обычно сопровождается hello **наступает** состояния, но может быть наличие условие или SplitOn команду в окне просмотра кода, не было выполнено.</span><span class="sxs-lookup"><span data-stu-id="4914b-121">This status is usually accompanied by hello **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="4914b-122">**Сбой**.</span><span class="sxs-lookup"><span data-stu-id="4914b-122">**Failed**.</span></span> <span data-ttu-id="4914b-123">Произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="4914b-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="4914b-124">Запуск триггера вручную</span><span class="sxs-lookup"><span data-stu-id="4914b-124">Start a trigger manually</span></span>

<span data-ttu-id="4914b-125">Toocheck приложения hello логику для триггера доступны немедленно, без повторения следующего hello, нажмите кнопку **триггер, выберите** в главной колонке hello tooforce проверку.</span><span class="sxs-lookup"><span data-stu-id="4914b-125">If you want hello logic app toocheck for an available trigger immediately without waiting for hello next recurrence, click **Select Trigger** on hello main blade tooforce a check.</span></span> <span data-ttu-id="4914b-126">Например если щелкнуть эту ссылку с триггером общего банка данных вызывает опроса tooimmediately hello рабочего процесса общего банка данных для новых файлов.</span><span class="sxs-lookup"><span data-stu-id="4914b-126">For example, clicking this link with a Dropbox trigger causes hello workflow tooimmediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="4914b-127">Журнал выполнения</span><span class="sxs-lookup"><span data-stu-id="4914b-127">Run history</span></span>

<span data-ttu-id="4914b-128">Каждое срабатывание триггера завершается запуском.</span><span class="sxs-lookup"><span data-stu-id="4914b-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="4914b-129">Сведения о запуске доступны из основного колонки hello, которая содержит многие подробности, которые помогут вам понять, что произошло при выполнении рабочего процесса hello.</span><span class="sxs-lookup"><span data-stu-id="4914b-129">You can access run information from hello main blade, which contains many details that can help you understand what happened during hello workflow.</span></span>

![Поиск hello, журнал выполнения][2]

<span data-ttu-id="4914b-131">Запуска выводится одно из следующих статусов hello.</span><span class="sxs-lookup"><span data-stu-id="4914b-131">A run displays one of hello following statuses:</span></span>

* <span data-ttu-id="4914b-132">**Успешно**.</span><span class="sxs-lookup"><span data-stu-id="4914b-132">**Succeeded**.</span></span> <span data-ttu-id="4914b-133">Все действия выполнены успешно.</span><span class="sxs-lookup"><span data-stu-id="4914b-133">All actions succeeded.</span></span> <span data-ttu-id="4914b-134">Если произошел сбой, сбой было обработано действие, которое произошло позже в рабочем процессе hello.</span><span class="sxs-lookup"><span data-stu-id="4914b-134">If a failure happened, that failure was handled by an action that occurred later in hello workflow.</span></span> <span data-ttu-id="4914b-135">То есть hello сбоя было обработано, действие, которое было задано toorun после сбоя действия.</span><span class="sxs-lookup"><span data-stu-id="4914b-135">That is, hello failure was handled by an action that was set toorun after a failed action.</span></span>
* <span data-ttu-id="4914b-136">**Сбой**.</span><span class="sxs-lookup"><span data-stu-id="4914b-136">**Failed**.</span></span> <span data-ttu-id="4914b-137">Хотя бы одно действие завершилось ошибкой, не может обработать действие позже в рабочем процессе hello.</span><span class="sxs-lookup"><span data-stu-id="4914b-137">At least one action had a failure that was not handled by an action later in hello workflow.</span></span>
* <span data-ttu-id="4914b-138">**Отменено**.</span><span class="sxs-lookup"><span data-stu-id="4914b-138">**Cancelled**.</span></span> <span data-ttu-id="4914b-139">Hello рабочий процесс был запущен, но получил запрос на отмену.</span><span class="sxs-lookup"><span data-stu-id="4914b-139">hello workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="4914b-140">**Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="4914b-140">**Running**.</span></span> <span data-ttu-id="4914b-141">сейчас выполняется рабочий процесс Hello.</span><span class="sxs-lookup"><span data-stu-id="4914b-141">hello workflow is currently running.</span></span> <span data-ttu-id="4914b-142">Это состояние может возникнуть для регулируемой рабочих процессов, или из-за текущей ценовой план hello.</span><span class="sxs-lookup"><span data-stu-id="4914b-142">This status might occur for throttled workflows, or because of hello current pricing plan.</span></span> <span data-ttu-id="4914b-143">Дополнительные сведения см. в разделе [действие ограничения на странице цен hello](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="4914b-143">For details, see [action limits on hello pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="4914b-144">Настройка диагностики (hello графиков, отображаемых в списке hello, журнал выполнения) также может предоставить сведения о любой регулирования события, которые происходят.</span><span class="sxs-lookup"><span data-stu-id="4914b-144">Configuring diagnostics (hello charts that appear under hello run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="4914b-145">Просматривая журнал выполнения, можно ознакомиться с подробностями процесса.</span><span class="sxs-lookup"><span data-stu-id="4914b-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="4914b-146">Выходные данные триггера</span><span class="sxs-lookup"><span data-stu-id="4914b-146">Trigger outputs</span></span>

<span data-ttu-id="4914b-147">Триггер генерирует Показать hello данные, полученные из триггера hello.</span><span class="sxs-lookup"><span data-stu-id="4914b-147">Trigger outputs show hello data that came from hello trigger.</span></span> <span data-ttu-id="4914b-148">Они помогут разобраться, все ли свойства возвращаются так, как требуется.</span><span class="sxs-lookup"><span data-stu-id="4914b-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="4914b-149">Если вы не понимаете некоторое содержимое, узнайте, как Azure Logic Apps [обрабатывает разные типы содержимого](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="4914b-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Примеры выводных данных триггера][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="4914b-151">Входные и выходные данные действия</span><span class="sxs-lookup"><span data-stu-id="4914b-151">Action inputs and outputs</span></span>

<span data-ttu-id="4914b-152">Вы можете перейти в hello входные и выходные данные, которые получены действие.</span><span class="sxs-lookup"><span data-stu-id="4914b-152">You can drill into hello inputs and outputs that an action received.</span></span> <span data-ttu-id="4914b-153">Эти данные полезен для понимания hello размера и формы hello выходов, а также для поиска сообщения об ошибках, которые были созданы.</span><span class="sxs-lookup"><span data-stu-id="4914b-153">This data is useful for understanding hello size and shape of hello outputs, and also for finding any error messages that might have been generated.</span></span>

![Входные и выходные данные действия][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="4914b-155">Среда отладки рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="4914b-155">Debug workflow runtime</span></span>

<span data-ttu-id="4914b-156">Вместе с мониторинг hello входов, выходов и триггеры для запуска, можно добавить некоторые tooa действия рабочего процесса, в процессе отладки.</span><span class="sxs-lookup"><span data-stu-id="4914b-156">Along with monitoring hello inputs, outputs, and triggers of a run, you could add some steps tooa workflow that help with debugging.</span></span> 
<span data-ttu-id="4914b-157">Например, вы можете включить в рабочий процесс такой мощный инструмент, как [RequestBin](http://requestb.in).</span><span class="sxs-lookup"><span data-stu-id="4914b-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="4914b-158">С помощью RequestBin, можно настроить HTTP запроса инспектора toodetermine hello точный размер, форму и формат HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="4914b-158">By using RequestBin, you can set up an HTTP request inspector toodetermine hello exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="4914b-159">Можно создать RequestBin и вставьте URL-адрес hello в приложении логику действие HTTP POST с содержимое тела, требуется tootest, например, выражение или другой выходные данные шага.</span><span class="sxs-lookup"><span data-stu-id="4914b-159">You can create a RequestBin and paste hello URL in a logic app HTTP POST action with body content that you want tootest, for example, an expression or another step output.</span></span> <span data-ttu-id="4914b-160">После запуска приложения hello логики можно обновить ваш toosee RequestBin, как было сформировано hello запроса при создании на основе ядра логики приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4914b-160">After you run hello logic app, you can refresh your RequestBin toosee how hello request was formed when generated from hello Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
