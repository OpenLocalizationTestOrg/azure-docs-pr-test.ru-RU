---
title: "hello tooUse aaaHow Engagement API для Windows Phone Silverlight"
description: "Как tooUse hello Engagement API для Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="07bc3-103">Как tooUse hello Engagement API для Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="07bc3-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="07bc3-104">Этот документ является документом надстройку toohello [как toointegrate Mobile Engagement в приложения Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="07bc3-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="07bc3-105">Он предоставляет сведения о как toouse hello Engagement API tooreport статистики вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="07bc3-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="07bc3-106">Если требуется только Engagement tooreport приложения сеансы, действия, сбои и технические сведения, а затем hello простым способом является toomake все вашей `PhoneApplicationPage` вложенные классы наследуют от hello `EngagementPage` класса.</span><span class="sxs-lookup"><span data-stu-id="07bc3-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="07bc3-107">Если требуется toodo дополнительные, например, если вам требуется tooreport приложения определенных событий, ошибок и задания или при наличии tooreport действия приложения по-другому, чем один реализованный в hello hello `EngagementPage` классов, то вы должны toouse hello Engagement API.</span><span class="sxs-lookup"><span data-stu-id="07bc3-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="07bc3-108">Hello Engagement API обеспечивается hello `EngagementAgent` класса.</span><span class="sxs-lookup"><span data-stu-id="07bc3-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="07bc3-109">Вы можете обратиться к методам toothose через `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="07bc3-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="07bc3-110">Даже если модуль агентом hello не был инициализирован, каждый вызов API toohello откладывается и будет выполнена повторно при hello доступен.</span><span class="sxs-lookup"><span data-stu-id="07bc3-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="07bc3-111">Основные понятия Engagement</span><span class="sxs-lookup"><span data-stu-id="07bc3-111">Engagement concepts</span></span>
<span data-ttu-id="07bc3-112">следующие элементы Hello уточнить hello Mobile Engagement и основные понятия для платформы Windows Phone hello.</span><span class="sxs-lookup"><span data-stu-id="07bc3-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="07bc3-113">`Session` и `Activity`</span><span class="sxs-lookup"><span data-stu-id="07bc3-113">`Session` and `Activity`</span></span>
<span data-ttu-id="07bc3-114">*Действия* обычно связана с одной страницы приложения hello, toosay hello *действия* начинается, когда страница приветствия отображается и прекращается после закрытия страницы приветствия: hello случае при hello Engagement SDK интегрирован с помощью hello `EngagementPage` класса.</span><span class="sxs-lookup"><span data-stu-id="07bc3-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="07bc3-115">Но *действия* может также осуществляться вручную с помощью Engagement API hello.</span><span class="sxs-lookup"><span data-stu-id="07bc3-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="07bc3-116">Это позволяет toosplit данной странице в несколько частей tooget sub, Дополнительные сведения о hello использование этой страницы (например tooknown как часто и как долго диалоговые окна используются внутри этой страницы).</span><span class="sxs-lookup"><span data-stu-id="07bc3-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="07bc3-117">Уведомление о действиях</span><span class="sxs-lookup"><span data-stu-id="07bc3-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="07bc3-118">Запуск нового действия пользователем</span><span class="sxs-lookup"><span data-stu-id="07bc3-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-119">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="07bc3-120">Требуется toocall `StartActivity()` каждое действие пользователя hello время изменяется.</span><span class="sxs-lookup"><span data-stu-id="07bc3-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="07bc3-121">функции Hello первый вызов toothis начинает новый сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="07bc3-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07bc3-122">пакет SDK для Hello автоматически метод hello действие завершения при закрытии приложения hello.</span><span class="sxs-lookup"><span data-stu-id="07bc3-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="07bc3-123">Таким образом настоятельно рекомендуется метод StartActivity toocall hello всякий раз, когда действие hello изменение пользователя hello и вызов tooNEVER hello метод действие завершения, с момента вызова этого метода заставляет toobe текущего сеанса hello завершено.</span><span class="sxs-lookup"><span data-stu-id="07bc3-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="07bc3-124">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="07bc3-125">Завершение текущего действия пользователем</span><span class="sxs-lookup"><span data-stu-id="07bc3-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-126">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="07bc3-127">Требуется toocall `EndActivity()` по крайней мере один раз в том случае, когда пользователь hello завершается его последнее действие.</span><span class="sxs-lookup"><span data-stu-id="07bc3-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="07bc3-128">Это позволяет сообщить hello Engagement SDK hello пользователя находится в режиме ожидания, что необходимость toobe hello пользовательский сеанс закрыт после hello время ожидания сеанса истекает (при вызове метода `StartActivity()` продолжается до истечения времени ожидания сеанса hello, просто hello сеанса).</span><span class="sxs-lookup"><span data-stu-id="07bc3-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="07bc3-129">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="07bc3-130">Уведомление о заданиях</span><span class="sxs-lookup"><span data-stu-id="07bc3-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="07bc3-131">Запустите задание</span><span class="sxs-lookup"><span data-stu-id="07bc3-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-132">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="07bc3-133">Tootrack certains hello рабочих заданий можно использовать за период времени.</span><span class="sxs-lookup"><span data-stu-id="07bc3-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="07bc3-134">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="07bc3-135">Конец задания</span><span class="sxs-lookup"><span data-stu-id="07bc3-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-136">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="07bc3-137">Сразу после завершения задачи, отслеживаются с помощью задания hello EndJob метод следует вызывать для данного задания, указав имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="07bc3-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="07bc3-138">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="07bc3-139">Уведомление о событиях</span><span class="sxs-lookup"><span data-stu-id="07bc3-139">Reporting Events</span></span>
<span data-ttu-id="07bc3-140">Существует три типа событий:</span><span class="sxs-lookup"><span data-stu-id="07bc3-140">There is three types of events :</span></span>

* <span data-ttu-id="07bc3-141">Изолированные события</span><span class="sxs-lookup"><span data-stu-id="07bc3-141">Standalone events</span></span>
* <span data-ttu-id="07bc3-142">События сеанса</span><span class="sxs-lookup"><span data-stu-id="07bc3-142">Session events</span></span>
* <span data-ttu-id="07bc3-143">События задания</span><span class="sxs-lookup"><span data-stu-id="07bc3-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="07bc3-144">Изолированные события</span><span class="sxs-lookup"><span data-stu-id="07bc3-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-145">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="07bc3-146">Автономный события могут происходить за пределами hello контекст сеанса.</span><span class="sxs-lookup"><span data-stu-id="07bc3-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="07bc3-147">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="07bc3-148">События сеанса</span><span class="sxs-lookup"><span data-stu-id="07bc3-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-149">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="07bc3-150">События сеанса — это обычно используется tooreport hello действия, выполняемые пользователем во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="07bc3-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="07bc3-151">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-151">Example</span></span>
<span data-ttu-id="07bc3-152">**Без данных:**</span><span class="sxs-lookup"><span data-stu-id="07bc3-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="07bc3-153">**С данными:**</span><span class="sxs-lookup"><span data-stu-id="07bc3-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="07bc3-154">События задания</span><span class="sxs-lookup"><span data-stu-id="07bc3-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-155">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="07bc3-156">Задания события, обычно используемых tooreport hello действия, выполняемые пользователем во время выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="07bc3-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="07bc3-157">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="07bc3-158">Уведомление об ошибках</span><span class="sxs-lookup"><span data-stu-id="07bc3-158">Reporting Errors</span></span>
<span data-ttu-id="07bc3-159">Существует три типа ошибок:</span><span class="sxs-lookup"><span data-stu-id="07bc3-159">There is three types of errors :</span></span>

* <span data-ttu-id="07bc3-160">Изолированные ошибки</span><span class="sxs-lookup"><span data-stu-id="07bc3-160">Standalone errors</span></span>
* <span data-ttu-id="07bc3-161">Ошибки сеанса</span><span class="sxs-lookup"><span data-stu-id="07bc3-161">Session errors</span></span>
* <span data-ttu-id="07bc3-162">Ошибки заданий</span><span class="sxs-lookup"><span data-stu-id="07bc3-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="07bc3-163">Изолированные ошибки</span><span class="sxs-lookup"><span data-stu-id="07bc3-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-164">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="07bc3-165">Ошибки противоположные toosession автономный ошибки могут возникать за пределами hello контекст сеанса.</span><span class="sxs-lookup"><span data-stu-id="07bc3-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="07bc3-166">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="07bc3-167">Ошибки сеанса</span><span class="sxs-lookup"><span data-stu-id="07bc3-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-168">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="07bc3-169">Ошибки сеанса это обычно используется tooreport hello ошибки, влияющие на hello пользователя во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="07bc3-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="07bc3-170">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="07bc3-171">Ошибки заданий</span><span class="sxs-lookup"><span data-stu-id="07bc3-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-172">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="07bc3-173">Ошибки могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="07bc3-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="07bc3-174">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="07bc3-175">Сбои отчетов</span><span class="sxs-lookup"><span data-stu-id="07bc3-175">Reporting Crashes</span></span>
<span data-ttu-id="07bc3-176">агент Hello предоставляет два toodeal методы сбоев.</span><span class="sxs-lookup"><span data-stu-id="07bc3-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="07bc3-177">Отправка исключения</span><span class="sxs-lookup"><span data-stu-id="07bc3-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-178">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="07bc3-179">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-179">Example</span></span>
<span data-ttu-id="07bc3-180">Исключение можно отправить в любое время, вызвав:</span><span class="sxs-lookup"><span data-stu-id="07bc3-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="07bc3-181">Также можно использовать сеанс необязательный параметр hello tooterminate engagement момент hello то же время, чем отправка hello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="07bc3-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="07bc3-182">Таким образом, вызов toodo:</span><span class="sxs-lookup"><span data-stu-id="07bc3-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="07bc3-183">Если это сделать, сеанс hello и заданий будет закрыто сразу после отправки hello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="07bc3-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="07bc3-184">Отправка необработанного исключения</span><span class="sxs-lookup"><span data-stu-id="07bc3-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="07bc3-185">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="07bc3-186">Engagement также предоставляет метод toosend необработанных исключений.</span><span class="sxs-lookup"><span data-stu-id="07bc3-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="07bc3-187">Это особенно полезно при использовании внутри обработчика событий UnhandledException hello silverlight.</span><span class="sxs-lookup"><span data-stu-id="07bc3-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="07bc3-188">Этот метод будет **всегда** завершить сеанс engagement hello и задания после вызова.</span><span class="sxs-lookup"><span data-stu-id="07bc3-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="07bc3-189">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-189">Example</span></span>
<span data-ttu-id="07bc3-190">Его можно использовать tooimplement собственный обработчик UnhandledException (особенно если вы отключили hello аварийного завершения автоматического компонент рвением отчетов).</span><span class="sxs-lookup"><span data-stu-id="07bc3-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="07bc3-191">Например, в hello `Application_UnhandledException` метод hello `App.xaml.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="07bc3-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="07bc3-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="07bc3-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="07bc3-193">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="07bc3-194">Когда пользователь hello вперед, выходит из приложения, после возникновения события деактивирован hello, hello операционной системы попытается tooput приложения hello в неактивное состояние.</span><span class="sxs-lookup"><span data-stu-id="07bc3-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="07bc3-195">Затем приложение hello — захоронение.</span><span class="sxs-lookup"><span data-stu-id="07bc3-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="07bc3-196">В этом процессе приложения прервана, но некоторые данные о состоянии hello приложения hello и hello отдельных страницах приложения hello сохраняется.</span><span class="sxs-lookup"><span data-stu-id="07bc3-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="07bc3-197">У вас есть tooinsert `EngagementAgent.Instance.OnActivated(e)` в hello `Application_Activated` метод hello App.xaml.cs файл tooreset hello Engagement агента после захоронено приложения hello.</span><span class="sxs-lookup"><span data-stu-id="07bc3-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="07bc3-198">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="07bc3-199">Идентификатор устройства</span><span class="sxs-lookup"><span data-stu-id="07bc3-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="07bc3-200">Идентификатор устройства engagement hello можно получить путем вызова данного метода.</span><span class="sxs-lookup"><span data-stu-id="07bc3-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="07bc3-201">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="07bc3-201">Extras parameters</span></span>
<span data-ttu-id="07bc3-202">Произвольные данные могут быть tooan вложенное событие, ошибка, действия или задания.</span><span class="sxs-lookup"><span data-stu-id="07bc3-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="07bc3-203">Эти данные можно структурировать по словарю.</span><span class="sxs-lookup"><span data-stu-id="07bc3-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="07bc3-204">Ключи и значения могут принадлежать к любому типу.</span><span class="sxs-lookup"><span data-stu-id="07bc3-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="07bc3-205">Вспомогательные элементы данных сериализуются, поэтому если требуется tooinsert свой собственный тип в дополнения tooadd контракт данных для этого типа.</span><span class="sxs-lookup"><span data-stu-id="07bc3-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="07bc3-206">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-206">Example</span></span>
<span data-ttu-id="07bc3-207">Создадим новый класс Person.</span><span class="sxs-lookup"><span data-stu-id="07bc3-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="07bc3-208">Затем мы добавим `Person` дополнительных tooan экземпляра.</span><span class="sxs-lookup"><span data-stu-id="07bc3-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="07bc3-209">Если поместить другие типы объектов, убедитесь, что их метода ToString() — реализовано tooreturn удобную для восприятия строку.</span><span class="sxs-lookup"><span data-stu-id="07bc3-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="07bc3-210">Ограничения</span><span class="sxs-lookup"><span data-stu-id="07bc3-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="07bc3-211">ключей</span><span class="sxs-lookup"><span data-stu-id="07bc3-211">Keys</span></span>
<span data-ttu-id="07bc3-212">Каждый ключ в hello объекта должно соответствовать hello следующее регулярное выражение:</span><span class="sxs-lookup"><span data-stu-id="07bc3-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="07bc3-213">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="07bc3-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="07bc3-214">Размер</span><span class="sxs-lookup"><span data-stu-id="07bc3-214">Size</span></span>
<span data-ttu-id="07bc3-215">Дополнения ограничены слишком**1024** знаков в каждом вызове.</span><span class="sxs-lookup"><span data-stu-id="07bc3-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="07bc3-216">Уведомление о данных приложения</span><span class="sxs-lookup"><span data-stu-id="07bc3-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="07bc3-217">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="07bc3-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="07bc3-218">Можно вручную сообщить отслеживания сведения (или любые другие сведения о приложении), с помощью функции SendAppInfo() hello.</span><span class="sxs-lookup"><span data-stu-id="07bc3-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="07bc3-219">Обратите внимание, что эти данные могут быть отосланы постепенно: hello только последнее значение для указанного ключа, которые будут храниться для данного устройства.</span><span class="sxs-lookup"><span data-stu-id="07bc3-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="07bc3-220">Как дополнения событий и использовать словарь\<объекта, объект\> tooattach сведения.</span><span class="sxs-lookup"><span data-stu-id="07bc3-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="07bc3-221">Пример</span><span class="sxs-lookup"><span data-stu-id="07bc3-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="07bc3-222">Ограничения</span><span class="sxs-lookup"><span data-stu-id="07bc3-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="07bc3-223">ключей</span><span class="sxs-lookup"><span data-stu-id="07bc3-223">Keys</span></span>
<span data-ttu-id="07bc3-224">Каждый ключ в hello объекта должно соответствовать hello следующее регулярное выражение:</span><span class="sxs-lookup"><span data-stu-id="07bc3-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="07bc3-225">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="07bc3-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="07bc3-226">Размер</span><span class="sxs-lookup"><span data-stu-id="07bc3-226">Size</span></span>
<span data-ttu-id="07bc3-227">Сведения о приложении ограничены слишком**1024** знаков в каждом вызове.</span><span class="sxs-lookup"><span data-stu-id="07bc3-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="07bc3-228">В hello предыдущего примера hello JSON, отправленных сервером toohello является 44 символов:</span><span class="sxs-lookup"><span data-stu-id="07bc3-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="07bc3-229">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="07bc3-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="07bc3-230">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="07bc3-230">Enable Logging</span></span>
<span data-ttu-id="07bc3-231">Hello SDK может быть настроенный tooproduce журналы тестирования в консоли hello интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="07bc3-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="07bc3-232">По умолчанию эти журналы не активированы.</span><span class="sxs-lookup"><span data-stu-id="07bc3-232">These logs are not activated by default.</span></span> <span data-ttu-id="07bc3-233">toocustomize hello, обновить свойство `EngagementAgent.Instance.TestLogEnabled` tooone hello значения, доступные из hello `EngagementTestLogLevel` перечисления, например:</span><span class="sxs-lookup"><span data-stu-id="07bc3-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
