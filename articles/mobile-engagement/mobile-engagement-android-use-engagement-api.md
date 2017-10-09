---
title: "hello tooUse aaaHow API Engagement для Android"
description: "Новейшую версию пакета SDK Android - как tooUse hello API Engagement для Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="fc801-103">Как tooUse hello API Engagement для Android</span><span class="sxs-lookup"><span data-stu-id="fc801-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="fc801-104">Этот документ является документом надстройку toohello [Reporting Дополнительные параметры для Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="fc801-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="fc801-105">Он предоставляет сведения о как toouse hello Engagement API tooreport статистики вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="fc801-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="fc801-106">Имейте в виду, что если требуется только Engagement tooreport приложения сеансы, действия, сбои и технические сведения, затем hello самым простым способом является toomake все вашей `Activity` вложенные классы наследуются от соответствующего hello `EngagementActivity` класса.</span><span class="sxs-lookup"><span data-stu-id="fc801-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="fc801-107">Если требуется toodo дополнительные, например, если вам требуется tooreport приложения определенных событий, ошибок и задания или при наличии tooreport действия приложения по-другому, чем один реализованный в hello hello `EngagementActivity` классов, то вы должны toouse hello Engagement API.</span><span class="sxs-lookup"><span data-stu-id="fc801-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="fc801-108">Hello Engagement API обеспечивается hello `EngagementAgent` класса.</span><span class="sxs-lookup"><span data-stu-id="fc801-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="fc801-109">Экземпляр этого класса можно получить путем вызова hello `EngagementAgent.getInstance(Context)` статическим методом (Обратите внимание, что hello `EngagementAgent` возвращаемый объект — единственное значение).</span><span class="sxs-lookup"><span data-stu-id="fc801-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="fc801-110">Основные понятия Engagement</span><span class="sxs-lookup"><span data-stu-id="fc801-110">Engagement concepts</span></span>
<span data-ttu-id="fc801-111">Hello следующие части уточнения hello Общие [Mobile Engagement концепции](mobile-engagement-concepts.md), для платформы Android hello.</span><span class="sxs-lookup"><span data-stu-id="fc801-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="fc801-112">`Session` и `Activity`</span><span class="sxs-lookup"><span data-stu-id="fc801-112">`Session` and `Activity`</span></span>
<span data-ttu-id="fc801-113">Если пользователь hello остается несколько секунд простоя между двумя *действия*, затем эта последовательность *действия* разбивается на два отдельных *сеансы*.</span><span class="sxs-lookup"><span data-stu-id="fc801-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="fc801-114">Эти несколько секунд, называются hello «время ожидания сеанса».</span><span class="sxs-lookup"><span data-stu-id="fc801-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="fc801-115">*Действия* обычно связана с одного экрана приложения hello, toosay hello *действия* начинается, когда экран приветствия отображается и останавливается при закрытии экрана приветствия: это hello случай, когда Hello Engagement SDK интегрирован с помощью hello `EngagementActivity` классы.</span><span class="sxs-lookup"><span data-stu-id="fc801-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="fc801-116">Но *действия* может также осуществляться вручную с помощью Engagement API hello.</span><span class="sxs-lookup"><span data-stu-id="fc801-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="fc801-117">Это позволяет toosplit указанными экранными несколько частей tooget sub, Дополнительные сведения о hello использования данного экрана (например tooknown как часто и как долго диалоговые окна используются внутри этот экран).</span><span class="sxs-lookup"><span data-stu-id="fc801-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="fc801-118">Уведомление о действиях</span><span class="sxs-lookup"><span data-stu-id="fc801-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fc801-119">Не требуется tooreport действий, как описано в этом разделе, если вы используете hello `EngagementActivity` класс и его вариантов, как описано в hello как tooIntegrate Engagement для Android документа.</span><span class="sxs-lookup"><span data-stu-id="fc801-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="fc801-120">Запуск нового действия пользователем</span><span class="sxs-lookup"><span data-stu-id="fc801-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="fc801-121">Требуется toocall `startActivity()` каждое действие пользователя hello время изменяется.</span><span class="sxs-lookup"><span data-stu-id="fc801-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="fc801-122">функции Hello первый вызов toothis начинает новый сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="fc801-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="fc801-123">Здравствуйте, наиболее toocall месте, эта функция используется для каждого действия `onResume` обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="fc801-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="fc801-124">Завершение текущего действия пользователем</span><span class="sxs-lookup"><span data-stu-id="fc801-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="fc801-125">Требуется toocall `endActivity()` по крайней мере один раз в том случае, когда пользователь hello завершается его последнее действие.</span><span class="sxs-lookup"><span data-stu-id="fc801-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="fc801-126">Это позволяет сообщить hello Engagement SDK hello пользователя находится в режиме ожидания, что необходимость toobe hello пользовательский сеанс закрыт после hello время ожидания сеанса истекает (Если вы вызываете `startActivity()` до истечения времени ожидания сеанса hello, просто возобновить сеанс hello).</span><span class="sxs-lookup"><span data-stu-id="fc801-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="fc801-127">Здравствуйте, наиболее toocall месте, эта функция используется для каждого действия `onPause` обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="fc801-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="fc801-128">Уведомление о событиях</span><span class="sxs-lookup"><span data-stu-id="fc801-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="fc801-129">События сеанса</span><span class="sxs-lookup"><span data-stu-id="fc801-129">Session events</span></span>
<span data-ttu-id="fc801-130">События сеанса — это обычно используется tooreport hello действия, выполняемые пользователем во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="fc801-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="fc801-131">**Пример без дополнительных данных:**</span><span class="sxs-lookup"><span data-stu-id="fc801-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="fc801-132">**Пример с дополнительными данными:**</span><span class="sxs-lookup"><span data-stu-id="fc801-132">**Example with extra data:**</span></span>

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a><span data-ttu-id="fc801-133">Изолированные события</span><span class="sxs-lookup"><span data-stu-id="fc801-133">Standalone Events</span></span>
<span data-ttu-id="fc801-134">События противоположные toosession автономный события могут происходить за пределами hello контекст сеанса.</span><span class="sxs-lookup"><span data-stu-id="fc801-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="fc801-135">**Пример**</span><span class="sxs-lookup"><span data-stu-id="fc801-135">**Example:**</span></span>

<span data-ttu-id="fc801-136">Предположим, что требуется tooreport события, происходящие при запуске широковещательных получателя:</span><span class="sxs-lookup"><span data-stu-id="fc801-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="fc801-137">Уведомление об ошибках</span><span class="sxs-lookup"><span data-stu-id="fc801-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="fc801-138">Ошибки сеанса</span><span class="sxs-lookup"><span data-stu-id="fc801-138">Session errors</span></span>
<span data-ttu-id="fc801-139">Ошибки сеанса это обычно используется tooreport hello ошибки, влияющие на hello пользователя во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="fc801-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="fc801-140">**Пример**</span><span class="sxs-lookup"><span data-stu-id="fc801-140">**Example:**</span></span>

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="fc801-141">Изолированные ошибки</span><span class="sxs-lookup"><span data-stu-id="fc801-141">Standalone errors</span></span>
<span data-ttu-id="fc801-142">Ошибки противоположные toosession автономный ошибки могут возникать за пределами hello контекст сеанса.</span><span class="sxs-lookup"><span data-stu-id="fc801-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="fc801-143">**Пример**</span><span class="sxs-lookup"><span data-stu-id="fc801-143">**Example:**</span></span>

<span data-ttu-id="fc801-144">Hello следующем примере показано, как работает tooreport ошибку при нехватке памяти hello на телефоне hello во время процесса приложения.</span><span class="sxs-lookup"><span data-stu-id="fc801-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="fc801-145">Уведомление о заданиях</span><span class="sxs-lookup"><span data-stu-id="fc801-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="fc801-146">Пример</span><span class="sxs-lookup"><span data-stu-id="fc801-146">Example</span></span>
<span data-ttu-id="fc801-147">Предположим, что требуется длительность hello tooreport процесс входа в систему:</span><span class="sxs-lookup"><span data-stu-id="fc801-147">Suppose you want tooreport hello duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="fc801-148">Уведомление об ошибках при выполнении задания</span><span class="sxs-lookup"><span data-stu-id="fc801-148">Report Errors during a Job</span></span>
<span data-ttu-id="fc801-149">Ошибки могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="fc801-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="fc801-150">**Пример**</span><span class="sxs-lookup"><span data-stu-id="fc801-150">**Example:**</span></span>

<span data-ttu-id="fc801-151">Предположим, что нужно tooreport Ошибка входа в систему процесс:</span><span class="sxs-lookup"><span data-stu-id="fc801-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="fc801-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="fc801-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="fc801-153">Отчеты о событиях во время выполнения задания</span><span class="sxs-lookup"><span data-stu-id="fc801-153">Reporting Events during a job</span></span>
<span data-ttu-id="fc801-154">События могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="fc801-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="fc801-155">**Пример**</span><span class="sxs-lookup"><span data-stu-id="fc801-155">**Example:**</span></span>

<span data-ttu-id="fc801-156">Предположим, что у нас есть социальных сетей, мы используем задания tooreport hello общее время во время которого hello пользователь является toohello подключенного сервера.</span><span class="sxs-lookup"><span data-stu-id="fc801-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="fc801-157">Hello пользователя может оставаться на связи в фоновом режиме даже в том случае, если он используется другим приложением или при hello телефон находится в спящем режиме, поэтому нет сеанса.</span><span class="sxs-lookup"><span data-stu-id="fc801-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="fc801-158">Hello пользователя может получать сообщения от его друзей, это событие задания.</span><span class="sxs-lookup"><span data-stu-id="fc801-158">hello user can receive messages from his friends, this is a job event.</span></span>

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a><span data-ttu-id="fc801-159">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="fc801-159">Extra parameters</span></span>
<span data-ttu-id="fc801-160">Произвольные данные могут быть вложенные tooevents, ошибок, действий и заданий.</span><span class="sxs-lookup"><span data-stu-id="fc801-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="fc801-161">Эти данные могут быть структурированы, здесь используется класс пакета Android (на самом деле он работает в качестве дополнительных параметров в целях Android).</span><span class="sxs-lookup"><span data-stu-id="fc801-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="fc801-162">Обратите внимание, что пакет может содержать массивы или экземпляры другого пакета.</span><span class="sxs-lookup"><span data-stu-id="fc801-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc801-163">Если поместить в параметрах parcelable или serializable, убедитесь, что их `toString()` метод является реализовано tooreturn читаемую пользователем строку.</span><span class="sxs-lookup"><span data-stu-id="fc801-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="fc801-164">Сериализуемые классы, содержащие непереходные поля, которые не сериализуются, приведут к сбою Android при вызове `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="fc801-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="fc801-165">Разреженные массивы в дополнительных параметрах не поддерживаются, то есть не сериализуется как массив.</span><span class="sxs-lookup"><span data-stu-id="fc801-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="fc801-166">Их следует преобразовать в стандартные массивы перед использованием в дополнительных параметрах.</span><span class="sxs-lookup"><span data-stu-id="fc801-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="fc801-167">Пример</span><span class="sxs-lookup"><span data-stu-id="fc801-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="fc801-168">Ограничения</span><span class="sxs-lookup"><span data-stu-id="fc801-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="fc801-169">ключей</span><span class="sxs-lookup"><span data-stu-id="fc801-169">Keys</span></span>
<span data-ttu-id="fc801-170">Каждый ключ в hello `Bundle` должно соответствовать hello следующее регулярное выражение:</span><span class="sxs-lookup"><span data-stu-id="fc801-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="fc801-171">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="fc801-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="fc801-172">Размер</span><span class="sxs-lookup"><span data-stu-id="fc801-172">Size</span></span>
<span data-ttu-id="fc801-173">Дополнения ограничены слишком**1024** символов на вызов (один раз в кодировке JSON службой Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="fc801-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="fc801-174">В hello предыдущего примера hello JSON, отправленных сервером toohello является 58 символов:</span><span class="sxs-lookup"><span data-stu-id="fc801-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="fc801-175">Уведомление о данных приложения</span><span class="sxs-lookup"><span data-stu-id="fc801-175">Reporting Application Information</span></span>
<span data-ttu-id="fc801-176">Можно вручную сообщить отслеживания сведения (или любые другие сведения о приложении), с помощью hello `sendAppInfo()` функции.</span><span class="sxs-lookup"><span data-stu-id="fc801-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="fc801-177">Обратите внимание, что эти данные могут быть отосланы постепенно: hello только последнее значение для указанного ключа, которые будут храниться для данного устройства.</span><span class="sxs-lookup"><span data-stu-id="fc801-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="fc801-178">Как дополнения событий hello класса набора сведений о приложении используется tooabstract, обратите внимание, что массивы или вложенным объединяет будет рассматриваться как плоский строки (с помощью сериализации JSON).</span><span class="sxs-lookup"><span data-stu-id="fc801-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="fc801-179">Пример</span><span class="sxs-lookup"><span data-stu-id="fc801-179">Example</span></span>
<span data-ttu-id="fc801-180">Ниже приведен Пол пользователя toosend образец кода и birthdate.</span><span class="sxs-lookup"><span data-stu-id="fc801-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="fc801-181">Ограничения</span><span class="sxs-lookup"><span data-stu-id="fc801-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="fc801-182">ключей</span><span class="sxs-lookup"><span data-stu-id="fc801-182">Keys</span></span>
<span data-ttu-id="fc801-183">Каждый ключ в hello `Bundle` должно соответствовать hello следующее регулярное выражение:</span><span class="sxs-lookup"><span data-stu-id="fc801-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="fc801-184">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="fc801-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="fc801-185">Размер</span><span class="sxs-lookup"><span data-stu-id="fc801-185">Size</span></span>
<span data-ttu-id="fc801-186">Сведения о приложении ограничены слишком**1024** символов на вызов (один раз в кодировке JSON службой Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="fc801-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="fc801-187">В hello предыдущего примера hello JSON, отправленных сервером toohello является 44 символов:</span><span class="sxs-lookup"><span data-stu-id="fc801-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
