---
title: "hello tooUse aaaHow Engagement API для iOS"
description: "Последние iOS SDK — как tooUse hello API участия в iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a><span data-ttu-id="a7a56-103">Как tooUse hello API участия в iOS</span><span class="sxs-lookup"><span data-stu-id="a7a56-103">How tooUse hello Engagement API on iOS</span></span>
<span data-ttu-id="a7a56-104">Этот документ является документом toohello надстройку как tooIntegrate Engagement на iOS: он предоставляет сведения о как toouse hello Engagement API tooreport статистики вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a7a56-104">This document is an add-on toohello document How tooIntegrate Engagement on iOS: it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="a7a56-105">Имейте в виду, что если требуется только Engagement tooreport приложения сеансы, действия, сбои и технические сведения, затем hello простой способ основан toomake всех пользовательских `UIViewController` объекты наследуют от соответствующего hello `EngagementViewController` класса .</span><span class="sxs-lookup"><span data-stu-id="a7a56-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your custom `UIViewController` objects inherit from hello corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="a7a56-106">Если требуется toodo дополнительные, например, если вам требуется tooreport приложения определенных событий, ошибок и задания или при наличии tooreport действия приложения по-другому, чем один реализованный в hello hello `EngagementViewController` классов, то вы должны toouse hello Engagement API.</span><span class="sxs-lookup"><span data-stu-id="a7a56-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementViewController` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="a7a56-107">Hello Engagement API обеспечивается hello `EngagementAgent` класса.</span><span class="sxs-lookup"><span data-stu-id="a7a56-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="a7a56-108">Экземпляр этого класса можно получить путем вызова hello `[EngagementAgent shared]` статическим методом (Обратите внимание, что hello `EngagementAgent` возвращаемый объект — единственное значение).</span><span class="sxs-lookup"><span data-stu-id="a7a56-108">An instance of this class can be retrieved by calling hello `[EngagementAgent shared]` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="a7a56-109">Прежде чем все вызовы API, hello `EngagementAgent` необходимо инициализировать объект с помощью вызова метода hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="a7a56-109">Before any API calls, hello `EngagementAgent` object must be initialized by calling hello method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="a7a56-110">Основные понятия Engagement</span><span class="sxs-lookup"><span data-stu-id="a7a56-110">Engagement concepts</span></span>
<span data-ttu-id="a7a56-111">Hello следующие части уточнения hello Общие [Mobile Engagement понятия](mobile-engagement-concepts.md) для платформы iOS hello.</span><span class="sxs-lookup"><span data-stu-id="a7a56-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="a7a56-112">`Session` и `Activity`</span><span class="sxs-lookup"><span data-stu-id="a7a56-112">`Session` and `Activity`</span></span>
<span data-ttu-id="a7a56-113">*Действия* обычно связана с одного экрана приложения hello, toosay hello *действия* начинается, когда экран приветствия отображается и останавливается при закрытии экрана приветствия: это hello случай, когда Hello Engagement SDK интегрирован с помощью hello `EngagementViewController` классы.</span><span class="sxs-lookup"><span data-stu-id="a7a56-113">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementViewController` classes.</span></span>

<span data-ttu-id="a7a56-114">Но *действия* может также осуществляться вручную с помощью Engagement API hello.</span><span class="sxs-lookup"><span data-stu-id="a7a56-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="a7a56-115">Это позволяет toosplit указанными экранными несколько частей tooget sub, Дополнительные сведения о hello использования данного экрана (например tooknown как часто и как долго диалоговые окна используются внутри этот экран).</span><span class="sxs-lookup"><span data-stu-id="a7a56-115">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="a7a56-116">Уведомление о действиях</span><span class="sxs-lookup"><span data-stu-id="a7a56-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="a7a56-117">Запуск нового действия пользователем</span><span class="sxs-lookup"><span data-stu-id="a7a56-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="a7a56-118">Требуется toocall `startActivity()` каждое действие пользователя hello время изменяется.</span><span class="sxs-lookup"><span data-stu-id="a7a56-118">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="a7a56-119">функции Hello первый вызов toothis начинает новый сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="a7a56-119">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="a7a56-120">Завершение текущего действия пользователем</span><span class="sxs-lookup"><span data-stu-id="a7a56-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="a7a56-121">Вы должны **никогда** эта функция вызывается в одиночку, за исключением того, если требуется, чтобы toosplit один из способов использования приложения в нескольких сеансах: вызов функции toothis приведет к завершению hello текущий сеанс немедленно, таким образом, следующий вызов слишком`startActivity()`начнет новый сеанс.</span><span class="sxs-lookup"><span data-stu-id="a7a56-121">You should **NEVER** call this function by yourself, except if you want toosplit one use of your application into several sessions: a call toothis function would end hello current session immediately, so, a subsequent call too`startActivity()` would start a new session.</span></span> <span data-ttu-id="a7a56-122">Эта функция автоматически вызывается hello SDK при закрытии приложения.</span><span class="sxs-lookup"><span data-stu-id="a7a56-122">This function is automatically called by hello SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="a7a56-123">Уведомление о событиях</span><span class="sxs-lookup"><span data-stu-id="a7a56-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="a7a56-124">События сеанса</span><span class="sxs-lookup"><span data-stu-id="a7a56-124">Session events</span></span>
<span data-ttu-id="a7a56-125">События сеанса — это обычно используется tooreport hello действия, выполняемые пользователем во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="a7a56-125">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="a7a56-126">**Пример без дополнительных данных:**</span><span class="sxs-lookup"><span data-stu-id="a7a56-126">**Example without extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

<span data-ttu-id="a7a56-127">**Пример с дополнительными данными:**</span><span class="sxs-lookup"><span data-stu-id="a7a56-127">**Example with extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="a7a56-128">Изолированные события</span><span class="sxs-lookup"><span data-stu-id="a7a56-128">Standalone events</span></span>
<span data-ttu-id="a7a56-129">Противоположные toosession события, события автономный может использоваться за пределами hello контекст сеанса.</span><span class="sxs-lookup"><span data-stu-id="a7a56-129">Contrary toosession events, standalone events can be used outside of hello context of a session.</span></span>

<span data-ttu-id="a7a56-130">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a7a56-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="a7a56-131">Уведомление об ошибках</span><span class="sxs-lookup"><span data-stu-id="a7a56-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="a7a56-132">Ошибки сеанса</span><span class="sxs-lookup"><span data-stu-id="a7a56-132">Session errors</span></span>
<span data-ttu-id="a7a56-133">Ошибки сеанса это обычно используется tooreport hello ошибки, влияющие на hello пользователя во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="a7a56-133">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="a7a56-134">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a7a56-134">**Example:**</span></span>

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="a7a56-135">Изолированные ошибки</span><span class="sxs-lookup"><span data-stu-id="a7a56-135">Standalone errors</span></span>
<span data-ttu-id="a7a56-136">Противоположные toosession ошибки, ошибки автономный может использоваться за пределами hello контекст сеанса.</span><span class="sxs-lookup"><span data-stu-id="a7a56-136">Contrary toosession errors, standalone errors can be used outside of hello context of a session.</span></span>

<span data-ttu-id="a7a56-137">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a7a56-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="a7a56-138">Уведомление о заданиях</span><span class="sxs-lookup"><span data-stu-id="a7a56-138">Reporting Jobs</span></span>
<span data-ttu-id="a7a56-139">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a7a56-139">**Example:**</span></span>

<span data-ttu-id="a7a56-140">Предположим, что требуется длительность hello tooreport процесс входа в систему:</span><span class="sxs-lookup"><span data-stu-id="a7a56-140">Suppose you want tooreport hello duration of your login process:</span></span>

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="a7a56-141">Уведомление об ошибках при выполнении задания</span><span class="sxs-lookup"><span data-stu-id="a7a56-141">Report Errors during a Job</span></span>
<span data-ttu-id="a7a56-142">Ошибки могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="a7a56-142">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="a7a56-143">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a7a56-143">**Example:**</span></span>

<span data-ttu-id="a7a56-144">Предположим, требуется tooreport ошибку во время процесса входа:</span><span class="sxs-lookup"><span data-stu-id="a7a56-144">Suppose you want tooreport an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a><span data-ttu-id="a7a56-145">События при выполнении задания</span><span class="sxs-lookup"><span data-stu-id="a7a56-145">Events during a job</span></span>
<span data-ttu-id="a7a56-146">События могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="a7a56-146">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="a7a56-147">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a7a56-147">**Example:**</span></span>

<span data-ttu-id="a7a56-148">Предположим, что у нас есть социальных сетей, мы используем задания tooreport hello общее время во время которого hello пользователь является toohello подключенного сервера.</span><span class="sxs-lookup"><span data-stu-id="a7a56-148">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="a7a56-149">Hello пользователя может получать сообщения от его друзей, это событие задания.</span><span class="sxs-lookup"><span data-stu-id="a7a56-149">hello user can receive messages from his friends, this is a job event.</span></span>

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a><span data-ttu-id="a7a56-150">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="a7a56-150">Extra parameters</span></span>
<span data-ttu-id="a7a56-151">Произвольные данные могут быть вложенные tooevents, ошибок, действий и заданий.</span><span class="sxs-lookup"><span data-stu-id="a7a56-151">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="a7a56-152">Эти данные могут быть структурированы. Они используют класс NSDictionary в iOS.</span><span class="sxs-lookup"><span data-stu-id="a7a56-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="a7a56-153">Обратите внимание, что дополнения могут содержать `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` или другие экземпляры `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="a7a56-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="a7a56-154">Hello дополнительный параметр сериализуется в JSON.</span><span class="sxs-lookup"><span data-stu-id="a7a56-154">hello extra parameter is serialized in JSON.</span></span> <span data-ttu-id="a7a56-155">Toopass различных объектов, чем hello описанных выше моделей, реализуйте следующий метод в классе hello:</span><span class="sxs-lookup"><span data-stu-id="a7a56-155">If you want toopass different objects than hello ones described above, you must implement hello following method in your class:</span></span>
> 
> <span data-ttu-id="a7a56-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="a7a56-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="a7a56-157">Hello метод должен возвращать JSON-представление объекта.</span><span class="sxs-lookup"><span data-stu-id="a7a56-157">hello method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="a7a56-158">Пример</span><span class="sxs-lookup"><span data-stu-id="a7a56-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="a7a56-159">Ограничения</span><span class="sxs-lookup"><span data-stu-id="a7a56-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="a7a56-160">ключей</span><span class="sxs-lookup"><span data-stu-id="a7a56-160">Keys</span></span>
<span data-ttu-id="a7a56-161">Каждый ключ в hello `NSDictionary` должно соответствовать hello следующее регулярное выражение:</span><span class="sxs-lookup"><span data-stu-id="a7a56-161">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="a7a56-162">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="a7a56-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a7a56-163">Размер</span><span class="sxs-lookup"><span data-stu-id="a7a56-163">Size</span></span>
<span data-ttu-id="a7a56-164">Дополнения ограничены слишком**1024** символов на вызов (один раз в кодировке JSON агентом Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="a7a56-164">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="a7a56-165">В hello предыдущего примера hello JSON, отправленных сервером toohello является 58 символов:</span><span class="sxs-lookup"><span data-stu-id="a7a56-165">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="a7a56-166">Уведомление о данных приложения</span><span class="sxs-lookup"><span data-stu-id="a7a56-166">Reporting Application Information</span></span>
<span data-ttu-id="a7a56-167">Можно вручную сообщить отслеживания сведения (или любые другие сведения о приложении), с помощью hello `sendAppInfo:` функции.</span><span class="sxs-lookup"><span data-stu-id="a7a56-167">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo:` function.</span></span>

<span data-ttu-id="a7a56-168">Обратите внимание, что эти данные могут быть отосланы постепенно: hello только последнее значение для указанного ключа, которые будут храниться для данного устройства.</span><span class="sxs-lookup"><span data-stu-id="a7a56-168">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="a7a56-169">Как дополнения событий hello `NSDictionary` класса используется tooabstract сведений о приложении, обратите внимание, что массивы или вложенные словарей будет рассматриваться как плоский строки (с помощью сериализации JSON).</span><span class="sxs-lookup"><span data-stu-id="a7a56-169">Like event extras, hello `NSDictionary` class is used tooabstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="a7a56-170">**Пример**</span><span class="sxs-lookup"><span data-stu-id="a7a56-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="a7a56-171">Ограничения</span><span class="sxs-lookup"><span data-stu-id="a7a56-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="a7a56-172">ключей</span><span class="sxs-lookup"><span data-stu-id="a7a56-172">Keys</span></span>
<span data-ttu-id="a7a56-173">Каждый ключ в hello `NSDictionary` должно соответствовать hello следующее регулярное выражение:</span><span class="sxs-lookup"><span data-stu-id="a7a56-173">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="a7a56-174">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="a7a56-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a7a56-175">Размер</span><span class="sxs-lookup"><span data-stu-id="a7a56-175">Size</span></span>
<span data-ttu-id="a7a56-176">Сведения о приложении ограничены слишком**1024** символов на вызов (один раз в кодировке JSON агентом Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="a7a56-176">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="a7a56-177">В hello предыдущего примера hello JSON, отправленных сервером toohello является 44 символов:</span><span class="sxs-lookup"><span data-stu-id="a7a56-177">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
