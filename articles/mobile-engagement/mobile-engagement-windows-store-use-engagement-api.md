---
title: "hello tooUse aaaHow Engagement API для Windows Universal."
description: "Как tooUse hello Engagement API для Windows Universal."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a><span data-ttu-id="e08e9-103">Как tooUse hello Engagement API для Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="e08e9-103">How tooUse hello Engagement API on Windows Universal</span></span>
<span data-ttu-id="e08e9-104">Этот документ является документом надстройку toohello [как tooIntegrate участия в универсальное приложение для Windows](mobile-engagement-windows-store-integrate-engagement.md): он предоставляет сведения о как toouse hello Engagement API tooreport статистике приложения.</span><span class="sxs-lookup"><span data-stu-id="e08e9-104">This document is an add-on toohello document [How tooIntegrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="e08e9-105">Имейте в виду, что если требуется только Engagement tooreport приложения сеансы, действия, сбои и технические сведения, затем hello самым простым способом является toomake все вашей `Page` вложенные классы наследуют от hello `EngagementPage` класса.</span><span class="sxs-lookup"><span data-stu-id="e08e9-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Page` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="e08e9-106">Если требуется toodo дополнительные, например, если вам требуется tooreport приложения определенных событий, ошибок и задания или при наличии tooreport действия приложения по-другому, чем один реализованный в hello hello `EngagementPage` классов, то вы должны toouse hello Engagement API.</span><span class="sxs-lookup"><span data-stu-id="e08e9-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="e08e9-107">Hello Engagement API обеспечивается hello `EngagementAgent` класса.</span><span class="sxs-lookup"><span data-stu-id="e08e9-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="e08e9-108">Вы можете обратиться к методам toothose через `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="e08e9-108">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="e08e9-109">Даже если модуль агентом hello не был инициализирован, каждый вызов API toohello откладывается и будет выполнена повторно при hello доступен.</span><span class="sxs-lookup"><span data-stu-id="e08e9-109">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="e08e9-110">Основные понятия Engagement</span><span class="sxs-lookup"><span data-stu-id="e08e9-110">Engagement concepts</span></span>
<span data-ttu-id="e08e9-111">Hello следующие части уточнения hello Общие [Mobile Engagement понятия](mobile-engagement-concepts.md) для платформы универсальных Windows hello.</span><span class="sxs-lookup"><span data-stu-id="e08e9-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="e08e9-112">`Session` и `Activity`</span><span class="sxs-lookup"><span data-stu-id="e08e9-112">`Session` and `Activity`</span></span>
<span data-ttu-id="e08e9-113">*Действия* обычно связана с одной страницы приложения hello, toosay hello *действия* начинается, когда страница приветствия отображается и прекращается после закрытия страницы приветствия: hello случае при hello Engagement SDK интегрирован с помощью hello `EngagementPage` класса.</span><span class="sxs-lookup"><span data-stu-id="e08e9-113">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="e08e9-114">Но *действия* может также осуществляться вручную с помощью Engagement API hello.</span><span class="sxs-lookup"><span data-stu-id="e08e9-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="e08e9-115">Это позволяет toosplit данной странице в нескольких sub tooget частей Дополнительные сведения об использовании hello этой страницы (например tooknow как часто и как долго диалоговые окна используются внутри этой страницы).</span><span class="sxs-lookup"><span data-stu-id="e08e9-115">This allows you toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknow how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="e08e9-116">Уведомление о действиях</span><span class="sxs-lookup"><span data-stu-id="e08e9-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="e08e9-117">Запуск нового действия пользователем</span><span class="sxs-lookup"><span data-stu-id="e08e9-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-118">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="e08e9-119">Требуется toocall `StartActivity()` каждое действие пользователя hello время изменяется.</span><span class="sxs-lookup"><span data-stu-id="e08e9-119">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="e08e9-120">функции Hello первый вызов toothis начинает новый сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="e08e9-120">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e08e9-121">пакет SDK для Hello автоматически вызывает метод hello действие завершения, при закрытии приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e08e9-121">hello SDK automatically calls hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="e08e9-122">Таким образом настоятельно рекомендуется метод StartActivity toocall hello всякий раз, когда меняется hello действий пользователя hello и завершен вызов tooNEVER hello метод действие завершения, с момента вызова этого метода заставляет toobe hello текущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="e08e9-122">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user changes, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="e08e9-123">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="e08e9-124">Завершение текущего действия пользователем</span><span class="sxs-lookup"><span data-stu-id="e08e9-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-125">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="e08e9-126">Действие hello и hello сеанс будет завершен.</span><span class="sxs-lookup"><span data-stu-id="e08e9-126">This ends hello activity and hello session.</span></span> <span data-ttu-id="e08e9-127">Не следует вызывать этот метод, если не вполне ясно, что он делает.</span><span class="sxs-lookup"><span data-stu-id="e08e9-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="e08e9-128">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="e08e9-129">Уведомление о заданиях</span><span class="sxs-lookup"><span data-stu-id="e08e9-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="e08e9-130">Запустите задание</span><span class="sxs-lookup"><span data-stu-id="e08e9-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-131">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="e08e9-132">Tootrack certains hello рабочих заданий можно использовать за период времени.</span><span class="sxs-lookup"><span data-stu-id="e08e9-132">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="e08e9-133">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-133">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="e08e9-134">Конец задания</span><span class="sxs-lookup"><span data-stu-id="e08e9-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-135">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="e08e9-136">Сразу после завершения задачи, отслеживаются с помощью задания hello EndJob метод следует вызывать для данного задания, указав имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="e08e9-136">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="e08e9-137">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-137">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="e08e9-138">Уведомление о событиях</span><span class="sxs-lookup"><span data-stu-id="e08e9-138">Reporting Events</span></span>
<span data-ttu-id="e08e9-139">Существует три типа событий:</span><span class="sxs-lookup"><span data-stu-id="e08e9-139">There is three types of events :</span></span>

* <span data-ttu-id="e08e9-140">Изолированные события</span><span class="sxs-lookup"><span data-stu-id="e08e9-140">Standalone events</span></span>
* <span data-ttu-id="e08e9-141">События сеанса</span><span class="sxs-lookup"><span data-stu-id="e08e9-141">Session events</span></span>
* <span data-ttu-id="e08e9-142">События задания</span><span class="sxs-lookup"><span data-stu-id="e08e9-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="e08e9-143">Изолированные события</span><span class="sxs-lookup"><span data-stu-id="e08e9-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-144">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="e08e9-145">Автономный события могут происходить за пределами hello контекст сеанса.</span><span class="sxs-lookup"><span data-stu-id="e08e9-145">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="e08e9-146">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="e08e9-147">События сеанса</span><span class="sxs-lookup"><span data-stu-id="e08e9-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-148">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="e08e9-149">События сеанса — это обычно используется tooreport hello действия, выполняемые пользователем во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="e08e9-149">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="e08e9-150">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-150">Example</span></span>
<span data-ttu-id="e08e9-151">**Без данных:**</span><span class="sxs-lookup"><span data-stu-id="e08e9-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="e08e9-152">**С данными:**</span><span class="sxs-lookup"><span data-stu-id="e08e9-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="e08e9-153">События задания</span><span class="sxs-lookup"><span data-stu-id="e08e9-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-154">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="e08e9-155">Задания события, обычно используемых tooreport hello действия, выполняемые пользователем во время выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="e08e9-155">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="e08e9-156">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="e08e9-157">Уведомление об ошибках</span><span class="sxs-lookup"><span data-stu-id="e08e9-157">Reporting Errors</span></span>
<span data-ttu-id="e08e9-158">Существует три типа ошибок:</span><span class="sxs-lookup"><span data-stu-id="e08e9-158">There are three types of errors :</span></span>

* <span data-ttu-id="e08e9-159">Изолированные ошибки</span><span class="sxs-lookup"><span data-stu-id="e08e9-159">Standalone errors</span></span>
* <span data-ttu-id="e08e9-160">Ошибки сеанса</span><span class="sxs-lookup"><span data-stu-id="e08e9-160">Session errors</span></span>
* <span data-ttu-id="e08e9-161">Ошибки заданий</span><span class="sxs-lookup"><span data-stu-id="e08e9-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="e08e9-162">Изолированные ошибки</span><span class="sxs-lookup"><span data-stu-id="e08e9-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-163">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="e08e9-164">Ошибки противоположные toosession автономный ошибки могут возникать за пределами hello контекст сеанса.</span><span class="sxs-lookup"><span data-stu-id="e08e9-164">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="e08e9-165">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="e08e9-166">Ошибки сеанса</span><span class="sxs-lookup"><span data-stu-id="e08e9-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-167">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="e08e9-168">Ошибки сеанса это обычно используется tooreport hello ошибки, влияющие на hello пользователя во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="e08e9-168">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="e08e9-169">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="e08e9-170">Ошибки заданий</span><span class="sxs-lookup"><span data-stu-id="e08e9-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-171">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="e08e9-172">Ошибки могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="e08e9-172">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="e08e9-173">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="e08e9-174">Сбои отчетов</span><span class="sxs-lookup"><span data-stu-id="e08e9-174">Reporting Crashes</span></span>
<span data-ttu-id="e08e9-175">агент Hello предоставляет два toodeal методы сбоев.</span><span class="sxs-lookup"><span data-stu-id="e08e9-175">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="e08e9-176">Отправка исключения</span><span class="sxs-lookup"><span data-stu-id="e08e9-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-177">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="e08e9-178">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-178">Example</span></span>
<span data-ttu-id="e08e9-179">Исключение можно отправить в любое время, вызвав:</span><span class="sxs-lookup"><span data-stu-id="e08e9-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="e08e9-180">Также можно использовать сеанс необязательный параметр hello tooterminate engagement момент hello то же время, чем отправка hello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="e08e9-180">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="e08e9-181">Таким образом, вызов toodo:</span><span class="sxs-lookup"><span data-stu-id="e08e9-181">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="e08e9-182">Если это сделать, сеанс hello и заданий будет закрыто сразу после отправки hello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="e08e9-182">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="e08e9-183">Отправка необработанного исключения</span><span class="sxs-lookup"><span data-stu-id="e08e9-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="e08e9-184">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="e08e9-185">Engagement предоставляет метод toosend необработанных исключений, если у вас есть **отключено** Engagement automatic **аварийного завершения** отчетов.</span><span class="sxs-lookup"><span data-stu-id="e08e9-185">Engagement also provides a method toosend unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="e08e9-186">Это особенно полезно при использовании внутри обработчика событий UnhandledException приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e08e9-186">This is especially useful when used inside hello application UnhandledException event handler.</span></span>

<span data-ttu-id="e08e9-187">Этот метод будет **всегда** завершить сеанс engagement hello и задания после вызова.</span><span class="sxs-lookup"><span data-stu-id="e08e9-187">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="e08e9-188">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-188">Example</span></span>
<span data-ttu-id="e08e9-189">Его можно использовать tooimplement UnhandledExceptionEventArgs обработчик.</span><span class="sxs-lookup"><span data-stu-id="e08e9-189">You can use it tooimplement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="e08e9-190">Например, добавить hello `Current_UnhandledException` метод hello `App.xaml.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="e08e9-190">For example, add hello `Current_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="e08e9-191">В файле App.xaml.cs в Public App(){} добавьте следующее:</span><span class="sxs-lookup"><span data-stu-id="e08e9-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="e08e9-192">Идентификатор устройства</span><span class="sxs-lookup"><span data-stu-id="e08e9-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="e08e9-193">Идентификатор устройства engagement hello можно получить путем вызова данного метода.</span><span class="sxs-lookup"><span data-stu-id="e08e9-193">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="e08e9-194">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="e08e9-194">Extras parameters</span></span>
<span data-ttu-id="e08e9-195">Произвольные данные могут быть tooan вложенное событие, ошибка, действия или задания.</span><span class="sxs-lookup"><span data-stu-id="e08e9-195">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="e08e9-196">Эти данные можно структурировать по словарю.</span><span class="sxs-lookup"><span data-stu-id="e08e9-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="e08e9-197">Ключи и значения могут принадлежать к любому типу.</span><span class="sxs-lookup"><span data-stu-id="e08e9-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="e08e9-198">Вспомогательные элементы данных сериализуются, поэтому если требуется tooinsert свой собственный тип в дополнения tooadd контракт данных для этого типа.</span><span class="sxs-lookup"><span data-stu-id="e08e9-198">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="e08e9-199">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-199">Example</span></span>
<span data-ttu-id="e08e9-200">Создадим новый класс Person.</span><span class="sxs-lookup"><span data-stu-id="e08e9-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="e08e9-201">Затем мы добавим `Person` дополнительных tooan экземпляра.</span><span class="sxs-lookup"><span data-stu-id="e08e9-201">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="e08e9-202">Если поместить другие типы объектов, убедитесь, что их метода ToString() — реализовано tooreturn удобную для восприятия строку.</span><span class="sxs-lookup"><span data-stu-id="e08e9-202">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="e08e9-203">Ограничения</span><span class="sxs-lookup"><span data-stu-id="e08e9-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="e08e9-204">ключей</span><span class="sxs-lookup"><span data-stu-id="e08e9-204">Keys</span></span>
<span data-ttu-id="e08e9-205">Каждый ключ в hello объекта должно соответствовать hello следующее регулярное выражение:</span><span class="sxs-lookup"><span data-stu-id="e08e9-205">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="e08e9-206">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="e08e9-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="e08e9-207">Размер</span><span class="sxs-lookup"><span data-stu-id="e08e9-207">Size</span></span>
<span data-ttu-id="e08e9-208">Дополнения ограничены слишком**1024** знаков в каждом вызове.</span><span class="sxs-lookup"><span data-stu-id="e08e9-208">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="e08e9-209">Уведомление о данных приложения</span><span class="sxs-lookup"><span data-stu-id="e08e9-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="e08e9-210">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e08e9-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="e08e9-211">Можно вручную сообщить отслеживания сведения (или любые другие сведения о приложении), с помощью функции SendAppInfo() hello.</span><span class="sxs-lookup"><span data-stu-id="e08e9-211">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="e08e9-212">Обратите внимание, что эти данные можно отправить постепенно: hello только последнее значение для указанного ключа, которые будут храниться для данного устройства.</span><span class="sxs-lookup"><span data-stu-id="e08e9-212">Note that this data can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="e08e9-213">Как дополнения событий и использовать словарь\<объекта, объект\> tooattach данных.</span><span class="sxs-lookup"><span data-stu-id="e08e9-213">Like event extras, use a Dictionary\<object, object\> tooattach data.</span></span>

### <a name="example"></a><span data-ttu-id="e08e9-214">Пример</span><span class="sxs-lookup"><span data-stu-id="e08e9-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="e08e9-215">Ограничения</span><span class="sxs-lookup"><span data-stu-id="e08e9-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="e08e9-216">ключей</span><span class="sxs-lookup"><span data-stu-id="e08e9-216">Keys</span></span>
<span data-ttu-id="e08e9-217">Каждый ключ в hello объекта должно соответствовать hello следующее регулярное выражение:</span><span class="sxs-lookup"><span data-stu-id="e08e9-217">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="e08e9-218">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="e08e9-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="e08e9-219">Размер</span><span class="sxs-lookup"><span data-stu-id="e08e9-219">Size</span></span>
<span data-ttu-id="e08e9-220">Сведения о приложении ограничено слишком**1024** знаков в каждом вызове.</span><span class="sxs-lookup"><span data-stu-id="e08e9-220">Application information is limited too**1024** characters per call.</span></span>

<span data-ttu-id="e08e9-221">В hello предыдущего примера hello JSON, отправленных сервером toohello является 44 символов:</span><span class="sxs-lookup"><span data-stu-id="e08e9-221">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="e08e9-222">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="e08e9-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="e08e9-223">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="e08e9-223">Enable Logging</span></span>
<span data-ttu-id="e08e9-224">Hello SDK может быть настроенный tooproduce журналы тестирования в консоли hello интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="e08e9-224">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="e08e9-225">По умолчанию эти журналы не активированы.</span><span class="sxs-lookup"><span data-stu-id="e08e9-225">These logs are not activated by default.</span></span> <span data-ttu-id="e08e9-226">toocustomize hello, обновить свойство `EngagementAgent.Instance.TestLogEnabled` tooone hello значения, доступные из hello `EngagementTestLogLevel` перечисления, например:</span><span class="sxs-lookup"><span data-stu-id="e08e9-226">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

