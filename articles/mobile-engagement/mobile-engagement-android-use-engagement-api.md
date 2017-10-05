---
title: "Использование API службы Engagement в Android"
description: "Последний пакет Android SDK - Использование API службы Engagement в Android"
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
ms.openlocfilehash: d353cd2fe47c54a0282cc5bb1b22b4a56e0cd82c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-android"></a><span data-ttu-id="0fddb-103">Использование API службы Engagement в Android</span><span class="sxs-lookup"><span data-stu-id="0fddb-103">How to Use the Engagement API on Android</span></span>
<span data-ttu-id="0fddb-104">Этот документ представляет собой дополнение к статье [Reporting Options with Engagement on Android](mobile-engagement-android-advanced-reporting.md)(Параметры отчетов для Служб мобильного взаимодействия на устройствах Android).</span><span class="sxs-lookup"><span data-stu-id="0fddb-104">This document is an add-on to the document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="0fddb-105">В нем рассказывается о том, как с помощью Engagement API предоставлять статистику по приложению.</span><span class="sxs-lookup"><span data-stu-id="0fddb-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="0fddb-106">Следует иметь в виду, что если вы хотите использовать службу Engagement только для получения отчетов о сеансах, действиях, сбоях и технической информации, проще всего сделать так, чтобы все подклассы `Activity` наследовались из класса `EngagementActivity`.</span><span class="sxs-lookup"><span data-stu-id="0fddb-106">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Activity` sub-classes inherit from the corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="0fddb-107">Если вы хотите, чтобы служба делала что-то еще, например сообщала о событиях, ошибках и заданиях приложения или сообщала о действиях приложения способом, отличным от реализованного в классах `EngagementActivity` , необходимо использовать API Engagement.</span><span class="sxs-lookup"><span data-stu-id="0fddb-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementActivity` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="0fddb-108">API Engagement предоставляется в классе `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="0fddb-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="0fddb-109">Экземпляр этого класса можно получить, вызвав статический метод `EngagementAgent.getInstance(Context)` (обратите внимание на то, что объект `EngagementAgent` возвращается в виде singleton).</span><span class="sxs-lookup"><span data-stu-id="0fddb-109">An instance of this class can be retrieved by calling the `EngagementAgent.getInstance(Context)` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="0fddb-110">Основные понятия Engagement</span><span class="sxs-lookup"><span data-stu-id="0fddb-110">Engagement concepts</span></span>
<span data-ttu-id="0fddb-111">В следующих подразделах дано более подробное объяснение [общих понятий Служб мобильного взаимодействия](mobile-engagement-concepts.md) для платформы Android.</span><span class="sxs-lookup"><span data-stu-id="0fddb-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for the Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="0fddb-112">`Session` и `Activity`</span><span class="sxs-lookup"><span data-stu-id="0fddb-112">`Session` and `Activity`</span></span>
<span data-ttu-id="0fddb-113">Если пользователь неактивен между двумя *действиями* больше чем несколько секунд, то последовательность его *действий* разбивается на два отдельных *сеанса*.</span><span class="sxs-lookup"><span data-stu-id="0fddb-113">If the user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="0fddb-114">Эти несколько секунд называются «время ожидания сеанса».</span><span class="sxs-lookup"><span data-stu-id="0fddb-114">These few seconds are called the "session timeout".</span></span>

<span data-ttu-id="0fddb-115">*Действие*, как правило, связано с одним экраном приложения, т. е. *действие* начинается при отображении экрана и завершается при его закрытии. Именно в таком случае пакет SDK для Engagement интегрируется с помощью класса `EngagementActivity`.</span><span class="sxs-lookup"><span data-stu-id="0fddb-115">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementActivity` classes.</span></span>

<span data-ttu-id="0fddb-116">*Действиями* можно также управлять вручную с помощью API Engagement.</span><span class="sxs-lookup"><span data-stu-id="0fddb-116">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="0fddb-117">Это позволяет разделить экран на несколько частей, чтобы получить дополнительную информацию об использовании этого экрана (например, информацию о частоте и продолжительности использования диалоговых окон на этом экране).</span><span class="sxs-lookup"><span data-stu-id="0fddb-117">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="0fddb-118">Уведомление о действиях</span><span class="sxs-lookup"><span data-stu-id="0fddb-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0fddb-119">В подготовке отчетов о действиях, как это описывается в данном разделе, нет необходимости, если используется класс `EngagementActivity` и его варианты, что рассматривается подробно в документе «Интеграция службы Engagement на Android».</span><span class="sxs-lookup"><span data-stu-id="0fddb-119">You don't need to report activities like described in this section if you are using the `EngagementActivity` class and its variants as explained in the How to Integrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="0fddb-120">Запуск нового действия пользователем</span><span class="sxs-lookup"><span data-stu-id="0fddb-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing the current activity is required for Reach to display in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="0fddb-121">При каждом изменении пользовательского действия необходимо вызывать `startActivity()` .</span><span class="sxs-lookup"><span data-stu-id="0fddb-121">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="0fddb-122">При первом вызове этой функции начинается новый сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="0fddb-122">The first call to this function starts a new user session.</span></span>

<span data-ttu-id="0fddb-123">Лучше всего вызывать данную функцию в обратном вызове каждого действия `onResume` .</span><span class="sxs-lookup"><span data-stu-id="0fddb-123">The best place to call this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="0fddb-124">Завершение текущего действия пользователем</span><span class="sxs-lookup"><span data-stu-id="0fddb-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="0fddb-125">Необходимо вызвать `endActivity()` как минимум один раз, когда пользователь заканчивает свое последнее действие.</span><span class="sxs-lookup"><span data-stu-id="0fddb-125">You need to call `endActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="0fddb-126">В результате пакет SDK для Engagement получает информацию о том, что пользователь неактивен и его сеанс необходимо закрыть после истечения времени ожидания (если вызов `startActivity()` сделан до этого момента, то сеанс просто возобновляется).</span><span class="sxs-lookup"><span data-stu-id="0fddb-126">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `startActivity()` before the session timeout expires, the session is simply resumed).</span></span>

<span data-ttu-id="0fddb-127">Лучше всего вызывать данную функцию в обратном вызове каждого действия `onPause` .</span><span class="sxs-lookup"><span data-stu-id="0fddb-127">The best place to call this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="0fddb-128">Уведомление о событиях</span><span class="sxs-lookup"><span data-stu-id="0fddb-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="0fddb-129">События сеанса</span><span class="sxs-lookup"><span data-stu-id="0fddb-129">Session events</span></span>
<span data-ttu-id="0fddb-130">События сеанса обычно используются для уведомления о действиях, выполняемых пользователем во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="0fddb-130">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="0fddb-131">**Пример без дополнительных данных:**</span><span class="sxs-lookup"><span data-stu-id="0fddb-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="0fddb-132">**Пример с дополнительными данными:**</span><span class="sxs-lookup"><span data-stu-id="0fddb-132">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="0fddb-133">Изолированные события</span><span class="sxs-lookup"><span data-stu-id="0fddb-133">Standalone Events</span></span>
<span data-ttu-id="0fddb-134">В отличие от событий сеанса изолированные события могут происходить вне контекста сеанса.</span><span class="sxs-lookup"><span data-stu-id="0fddb-134">Contrary to session events, standalone events can occur outside of the context of a session.</span></span>

<span data-ttu-id="0fddb-135">**Пример**</span><span class="sxs-lookup"><span data-stu-id="0fddb-135">**Example:**</span></span>

<span data-ttu-id="0fddb-136">Предположим, что требуется отчет о событиях, возникающих при активации получателя рассылки:</span><span class="sxs-lookup"><span data-stu-id="0fddb-136">Suppose you want to report events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="0fddb-137">Уведомление об ошибках</span><span class="sxs-lookup"><span data-stu-id="0fddb-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="0fddb-138">Ошибки сеанса</span><span class="sxs-lookup"><span data-stu-id="0fddb-138">Session errors</span></span>
<span data-ttu-id="0fddb-139">Ошибки сеанса обычно используются для уведомления об ошибках, влияющих на пользователя во время сеанса.</span><span class="sxs-lookup"><span data-stu-id="0fddb-139">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="0fddb-140">**Пример**</span><span class="sxs-lookup"><span data-stu-id="0fddb-140">**Example:**</span></span>

            /** The user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* The user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="0fddb-141">Изолированные ошибки</span><span class="sxs-lookup"><span data-stu-id="0fddb-141">Standalone errors</span></span>
<span data-ttu-id="0fddb-142">В отличие от ошибок сеанса изолированные ошибки могут возникать вне контекста сеанса.</span><span class="sxs-lookup"><span data-stu-id="0fddb-142">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

<span data-ttu-id="0fddb-143">**Пример**</span><span class="sxs-lookup"><span data-stu-id="0fddb-143">**Example:**</span></span>

<span data-ttu-id="0fddb-144">В следующем примере показано, как создать отчет об ошибке при нехватке памяти на телефоне во время выполнения процесса приложения.</span><span class="sxs-lookup"><span data-stu-id="0fddb-144">The following example shows how to report an error whenever the memory becomes low on the phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="0fddb-145">Уведомление о заданиях</span><span class="sxs-lookup"><span data-stu-id="0fddb-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="0fddb-146">Пример</span><span class="sxs-lookup"><span data-stu-id="0fddb-146">Example</span></span>
<span data-ttu-id="0fddb-147">Предположим, что вам необходимо сообщить о продолжительности процесса входа в систему:</span><span class="sxs-lookup"><span data-stu-id="0fddb-147">Suppose you want to report the duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="0fddb-148">Уведомление об ошибках при выполнении задания</span><span class="sxs-lookup"><span data-stu-id="0fddb-148">Report Errors during a Job</span></span>
<span data-ttu-id="0fddb-149">Ошибки могут быть связаны с выполняемым заданием, а не с текущим сеансом пользователя.</span><span class="sxs-lookup"><span data-stu-id="0fddb-149">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="0fddb-150">**Пример**</span><span class="sxs-lookup"><span data-stu-id="0fddb-150">**Example:**</span></span>

<span data-ttu-id="0fddb-151">Предположим, что нужно включить в отчет ошибку, которая возникает во время процесса входа в систему:</span><span class="sxs-lookup"><span data-stu-id="0fddb-151">Suppose you want to report an error during you login process:</span></span>

<span data-ttu-id="0fddb-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="0fddb-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try to sign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report the error to Engagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="0fddb-153">Отчеты о событиях во время выполнения задания</span><span class="sxs-lookup"><span data-stu-id="0fddb-153">Reporting Events during a job</span></span>
<span data-ttu-id="0fddb-154">События могут быть связаны с выполняемым заданием, а не с текущим сеансом пользователя.</span><span class="sxs-lookup"><span data-stu-id="0fddb-154">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="0fddb-155">**Пример**</span><span class="sxs-lookup"><span data-stu-id="0fddb-155">**Example:**</span></span>

<span data-ttu-id="0fddb-156">Предположим, что у нас есть социальная сеть, и мы используем задание, чтобы сообщить об общем времени подключения пользователя к серверу.</span><span class="sxs-lookup"><span data-stu-id="0fddb-156">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="0fddb-157">Пользователь может оставаться подключенных в фоновом режиме, даже если он использует другое приложение или телефон находится в спящем режиме, и поэтому сеанс отсутствует.</span><span class="sxs-lookup"><span data-stu-id="0fddb-157">The user can stay connected in background even when he's using another application or when the phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="0fddb-158">Пользователь может получить сообщения от своих друзей. Это и есть событием задания.</span><span class="sxs-lookup"><span data-stu-id="0fddb-158">The user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="0fddb-159">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="0fddb-159">Extra parameters</span></span>
<span data-ttu-id="0fddb-160">Произвольные данные можно прикрепить к событиям, ошибкам, действиям и заданиям.</span><span class="sxs-lookup"><span data-stu-id="0fddb-160">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="0fddb-161">Эти данные могут быть структурированы, здесь используется класс пакета Android (на самом деле он работает в качестве дополнительных параметров в целях Android).</span><span class="sxs-lookup"><span data-stu-id="0fddb-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="0fddb-162">Обратите внимание, что пакет может содержать массивы или экземпляры другого пакета.</span><span class="sxs-lookup"><span data-stu-id="0fddb-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0fddb-163">Если вы добавляете разбиваемые на пакеты или сериализуемые параметры, необходимо обеспечить реализацию их метода `toString()`, чтобы он возвращал понятную пользователю строку.</span><span class="sxs-lookup"><span data-stu-id="0fddb-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented to return a human-readable string.</span></span> <span data-ttu-id="0fddb-164">Сериализуемые классы, содержащие непереходные поля, которые не сериализуются, приведут к сбою Android при вызове `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="0fddb-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="0fddb-165">Разреженные массивы в дополнительных параметрах не поддерживаются, то есть не сериализуется как массив.</span><span class="sxs-lookup"><span data-stu-id="0fddb-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="0fddb-166">Их следует преобразовать в стандартные массивы перед использованием в дополнительных параметрах.</span><span class="sxs-lookup"><span data-stu-id="0fddb-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="0fddb-167">Пример</span><span class="sxs-lookup"><span data-stu-id="0fddb-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="0fddb-168">Ограничения</span><span class="sxs-lookup"><span data-stu-id="0fddb-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="0fddb-169">ключей</span><span class="sxs-lookup"><span data-stu-id="0fddb-169">Keys</span></span>
<span data-ttu-id="0fddb-170">Каждый ключ в `Bundle` должен соответствовать следующему регулярному выражению:</span><span class="sxs-lookup"><span data-stu-id="0fddb-170">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="0fddb-171">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="0fddb-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="0fddb-172">Размер</span><span class="sxs-lookup"><span data-stu-id="0fddb-172">Size</span></span>
<span data-ttu-id="0fddb-173">Длина дополнений ограничена **1024** знаками на один вызов (после кодирования в JSON-файле службой Engagement).</span><span class="sxs-lookup"><span data-stu-id="0fddb-173">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="0fddb-174">В предыдущем примере длина JSON-файла, отправленного на сервер, составляет 58 знаков:</span><span class="sxs-lookup"><span data-stu-id="0fddb-174">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="0fddb-175">Уведомление о данных приложения</span><span class="sxs-lookup"><span data-stu-id="0fddb-175">Reporting Application Information</span></span>
<span data-ttu-id="0fddb-176">С помощью функции `sendAppInfo()` вы можете вручную сообщать о данных отслеживания (или любых других данных о приложении).</span><span class="sxs-lookup"><span data-stu-id="0fddb-176">You can manually report tracking information (or any other application specific information) using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="0fddb-177">Обратите внимание, что такие данные можно отправлять поэтапно, так как для заданного устройства будет сохраняться только последнее значение заданного ключа.</span><span class="sxs-lookup"><span data-stu-id="0fddb-177">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="0fddb-178">как и при дополнительных событиях класс пакета используется для получения абстрактных сведений о приложении. Отметим, что массивы или вложенные пакеты будут считаться плоскими строками (с использованием сериализации JSON).</span><span class="sxs-lookup"><span data-stu-id="0fddb-178">Like event extras, the Bundle class is used to abstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="0fddb-179">Пример</span><span class="sxs-lookup"><span data-stu-id="0fddb-179">Example</span></span>
<span data-ttu-id="0fddb-180">Ниже приведен пример кода для отправки пола и даты рождения пользователя.</span><span class="sxs-lookup"><span data-stu-id="0fddb-180">Here is a code sample to send user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="0fddb-181">Ограничения</span><span class="sxs-lookup"><span data-stu-id="0fddb-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="0fddb-182">ключей</span><span class="sxs-lookup"><span data-stu-id="0fddb-182">Keys</span></span>
<span data-ttu-id="0fddb-183">Каждый ключ в `Bundle` должен соответствовать следующему регулярному выражению:</span><span class="sxs-lookup"><span data-stu-id="0fddb-183">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="0fddb-184">Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).</span><span class="sxs-lookup"><span data-stu-id="0fddb-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="0fddb-185">Размер</span><span class="sxs-lookup"><span data-stu-id="0fddb-185">Size</span></span>
<span data-ttu-id="0fddb-186">Данные приложения ограничены **1024** знаками на один вызов (после кодирования в JSON-файле службой Engagement).</span><span class="sxs-lookup"><span data-stu-id="0fddb-186">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="0fddb-187">В предыдущем примере длина JSON-файла, отправленного на сервер, составляет 44 знака:</span><span class="sxs-lookup"><span data-stu-id="0fddb-187">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
